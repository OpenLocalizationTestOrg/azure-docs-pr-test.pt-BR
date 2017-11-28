---
title: aaaDevelop para armazenamento de arquivo do Azure com C++ | Microsoft Docs
description: "Saiba como toodevelop C++ de aplicativos e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="a1634-103">Desenvolvimento para o Armazenamento de Arquivos do Azure com o C++</span><span class="sxs-lookup"><span data-stu-id="a1634-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="a1634-104">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="a1634-104">About this tutorial</span></span>

<span data-ttu-id="a1634-105">Neste tutorial, você aprenderá como operações básicas de tooperform no armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1634-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="a1634-106">Por meio de exemplos escritos em C++, você aprenderá como toocreate compartilhamentos e diretórios, carregar, listar e excluir arquivos.</span><span class="sxs-lookup"><span data-stu-id="a1634-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="a1634-107">Se você for novo armazenamento de arquivo tooAzure, passando por conceitos Olá Olá próximas seções será útil na compreensão exemplos hello.</span><span class="sxs-lookup"><span data-stu-id="a1634-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="a1634-108">Criar e excluir Compartilhamentos de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="a1634-109">Criar e excluir diretórios</span><span class="sxs-lookup"><span data-stu-id="a1634-109">Create and delete directories</span></span>
* <span data-ttu-id="a1634-110">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="a1634-111">Carregar, baixar e excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="a1634-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="a1634-112">Definir uma cota de saudação (tamanho máximo) para um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="a1634-113">Crie uma assinatura de acesso compartilhado (chave SAS) para um arquivo que usa uma política de acesso compartilhado definida no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="a1634-114">Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando funções e classes de e/s de C++ padrão hello.</span><span class="sxs-lookup"><span data-stu-id="a1634-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="a1634-115">Este artigo descreve como toowrite os aplicativos que usam Olá SDK de C++ de armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a1634-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="a1634-116">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="a1634-116">Create a C++ application</span></span>
<span data-ttu-id="a1634-117">exemplos de saudação toobuild, você precisará Olá tooinstall 2.4.0 de biblioteca de cliente de armazenamento do Azure para C++.</span><span class="sxs-lookup"><span data-stu-id="a1634-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="a1634-118">Você também deverá ter criado uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1634-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="a1634-119">Olá tooinstall 2.4.0 do cliente de armazenamento do Azure para C++, você pode usar um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a1634-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="a1634-120">**Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="a1634-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="a1634-121">**Windows:** no Visual Studio, clique em **Ferramentas &gt; Gerenciador de Pacotes do NuGet &gt; Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="a1634-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="a1634-122">Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1634-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="a1634-123">Configurar seu aplicativo toouse armazenamento de arquivo do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="a1634-124">Adicione a seguinte Olá incluem superior de toohello instruções Olá C++ do arquivo de origem em que você deseja que o armazenamento de arquivo do Azure toomanipulate:</span><span class="sxs-lookup"><span data-stu-id="a1634-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="a1634-125">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="a1634-126">toouse o armazenamento de arquivos, você precisa de conta de armazenamento do Azure de tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="a1634-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="a1634-127">Olá primeira etapa seria tooconfigure uma cadeia de conexão, que vamos usar conta de armazenamento do tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="a1634-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="a1634-128">Vamos definir uma toodo variável estática que.</span><span class="sxs-lookup"><span data-stu-id="a1634-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="a1634-129">Conectar-se a conta de armazenamento do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="a1634-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="a1634-130">Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a1634-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="a1634-131">tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="a1634-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="a1634-132">Criar um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-132">Create an Azure File share</span></span>
<span data-ttu-id="a1634-133">Todos os arquivos e diretórios do Armazenamento de Arquivos do Azure residem em um contêiner chamado **Compartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="a1634-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="a1634-134">Sua conta de armazenamento pode a quantidade de compartilhamentos que a capacidade da conta permitir.</span><span class="sxs-lookup"><span data-stu-id="a1634-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="a1634-135">compartilhamento de tooa tooobtain acesso e seu conteúdo, você precisa toouse um cliente de armazenamento do arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1634-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="a1634-136">Usando o cliente de armazenamento do Azure arquivo hello, em seguida, você pode obter um compartilhamento de tooa de referência.</span><span class="sxs-lookup"><span data-stu-id="a1634-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="a1634-137">compartilhamento de saudação toocreate, use Olá **create_if_not_exists** método hello **cloud_file_share** objeto.</span><span class="sxs-lookup"><span data-stu-id="a1634-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="a1634-138">Neste ponto, **compartilhar** contém um compartilhamento de tooa de referência chamado **compartilhamento meu exemplo**.</span><span class="sxs-lookup"><span data-stu-id="a1634-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="a1634-139">Excluir um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-139">Delete an Azure File share</span></span>
<span data-ttu-id="a1634-140">Excluir um compartilhamento é feito através da chamada hello **delete_if_exists** método em um objeto cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="a1634-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="a1634-141">O código fornecido a seguir é um exemplo de como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="a1634-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="a1634-142">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="a1634-142">Create a directory</span></span>
<span data-ttu-id="a1634-143">Você pode organizar o armazenamento, colocando arquivos em subpastas em vez de ter todos eles no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="a1634-144">Armazenamento de arquivo do Azure permite que você toocreate como permitir que vários diretórios como será sua conta.</span><span class="sxs-lookup"><span data-stu-id="a1634-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="a1634-145">saudação de código abaixo cria um diretório chamado **meu diretório de exemplo** sob diretório raiz de hello, bem como uma subpasta chamada **meu subdiretório de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="a1634-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="a1634-146">Excluir um diretório</span><span class="sxs-lookup"><span data-stu-id="a1634-146">Delete a directory</span></span>
<span data-ttu-id="a1634-147">Excluir um diretório é uma tarefa simples, embora deva-se observar que não é possível excluir um diretório que ainda contenha arquivos ou outros diretórios.</span><span class="sxs-lookup"><span data-stu-id="a1634-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="a1634-148">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="a1634-149">A lista de arquivos e diretórios em um compartilhamento pode ser obtida facilmente chamando **list_files_and_directories** em uma referência **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="a1634-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="a1634-150">tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **list_file_and_directory_item**, você deve chamar hello **list_file_and_directory_item.as_file** método tooget um **cloud_ arquivo** objeto ou hello **list_file_and_directory_item.as_directory** método tooget um **cloud_file_directory** objeto.</span><span class="sxs-lookup"><span data-stu-id="a1634-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="a1634-151">saudação de código a seguir demonstra como tooretrieve e saída Olá URI de cada item no diretório raiz de saudação do compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="a1634-152">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="a1634-152">Upload a file</span></span>
<span data-ttu-id="a1634-153">No hello muito menos, um compartilhamento de arquivos do Azure contém um diretório raiz onde os arquivos podem residir.</span><span class="sxs-lookup"><span data-stu-id="a1634-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="a1634-154">Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.</span><span class="sxs-lookup"><span data-stu-id="a1634-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="a1634-155">a primeira etapa Olá no carregamento de um arquivo é tooobtain um diretório de toohello de referência em que ele deve residir.</span><span class="sxs-lookup"><span data-stu-id="a1634-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="a1634-156">Para fazer isso, Olá chamada **get_root_directory_reference** método do objeto de compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="a1634-157">Agora que você tem um diretório de raiz de toohello de referência do compartilhamento hello, você pode carregar um arquivo para ele.</span><span class="sxs-lookup"><span data-stu-id="a1634-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="a1634-158">Este exemplo carrega de um arquivo, de um texto e de um fluxo.</span><span class="sxs-lookup"><span data-stu-id="a1634-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="a1634-159">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="a1634-159">Download a file</span></span>
<span data-ttu-id="a1634-160">arquivos toodownload, recuperar uma referência de arquivo e, em seguida, chamar hello **download_to_stream** método tootransfer Olá arquivo conteúdo tooa objeto de fluxo, que, em seguida, você pode manter arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="a1634-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="a1634-161">Como alternativa, você pode usar o hello **download_to_file** conteúdo de saudação do método toodownload um arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="a1634-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="a1634-162">Você pode usar o hello **download_text** conteúdo de saudação do método toodownload de um arquivo como uma cadeia de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="a1634-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="a1634-163">Olá, exemplo a seguir usa Olá **download_to_stream** e **download_text** toodemonstrate métodos baixando arquivos hello, que foram criados nas seções anteriores.</span><span class="sxs-lookup"><span data-stu-id="a1634-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="a1634-164">Excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="a1634-164">Delete a file</span></span>
<span data-ttu-id="a1634-165">Outra operação comum do Armazenamento de Arquivos do Azure é a exclusão de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a1634-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="a1634-166">Olá código a seguir exclui um arquivo chamado Meu-exemplo-arquivo-3 armazenados no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="a1634-167">Definir uma cota de saudação (tamanho máximo) para um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="a1634-168">Você pode definir cotas de hello (ou o tamanho máximo) para um compartilhamento de arquivo, em gigabytes.</span><span class="sxs-lookup"><span data-stu-id="a1634-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="a1634-169">Você também pode verificar toosee a quantidade de dados é atualmente armazenado no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="a1634-170">Pela configuração cota Olá para um compartilhamento, você pode limitar o tamanho total de Olá Olá arquivos armazenados no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="a1634-171">Se excede o tamanho total de saudação de arquivos no compartilhamento de saudação cota Olá definidos no compartilhamento de saudação, os clientes serão tooincrease não é possível Olá tamanho dos arquivos existentes ou criar novos arquivos, a menos que esses arquivos estão vazios.</span><span class="sxs-lookup"><span data-stu-id="a1634-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="a1634-172">exemplo Hello abaixo mostra como toocheck Olá uso atual para um compartilhamento e como tooset Olá cota para compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1634-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="a1634-173">Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="a1634-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="a1634-174">Você pode gerar uma SAS (assinatura de acesso compartilhado) para um compartilhamento de arquivo ou para um arquivo individual.</span><span class="sxs-lookup"><span data-stu-id="a1634-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="a1634-175">Você pode também criar uma política de acesso compartilhado um acesso de toomanage compartilhado de compartilhamento de arquivo assinaturas.</span><span class="sxs-lookup"><span data-stu-id="a1634-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="a1634-176">Criar uma política de acesso compartilhado é recomendada, pois ele fornece um meio de revogar Olá SAS se ela deve ser comprometida.</span><span class="sxs-lookup"><span data-stu-id="a1634-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="a1634-177">saudação de exemplo a seguir cria uma política de acesso compartilhado em um compartilhamento e usa que compartilham tooprovide Olá restrições para uma SAS em um arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="a1634-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="a1634-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1634-178">Next steps</span></span>
<span data-ttu-id="a1634-179">toolearn mais sobre o armazenamento do Azure, explore esses recursos:</span><span class="sxs-lookup"><span data-stu-id="a1634-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="a1634-180">Biblioteca do Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="a1634-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="a1634-181">[Exemplos de Serviço de Arquivo do Armazenamento do Azure no C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="a1634-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="a1634-182">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="a1634-183">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a1634-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)