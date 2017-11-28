---
title: aaaDevelop para armazenamento de arquivo do Azure com Java | Microsoft Docs
description: "Saiba como aplicativos do Java toodevelop e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="ea5f4-103">Desenvolvimento para o Armazenamento de Arquivos do Azure com Java</span><span class="sxs-lookup"><span data-stu-id="ea5f4-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="ea5f4-104">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="ea5f4-104">About this tutorial</span></span>
<span data-ttu-id="ea5f4-105">Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do Java toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="ea5f4-106">Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento de Java e o arquivo do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea5f4-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="ea5f4-107">Criar e excluir Compartilhamentos de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="ea5f4-108">Criar e excluir diretórios</span><span class="sxs-lookup"><span data-stu-id="ea5f4-108">Create and delete directories</span></span>
* <span data-ttu-id="ea5f4-109">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="ea5f4-110">Carregar, baixar e excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="ea5f4-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="ea5f4-111">Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando classes de e/s de Java padrão hello.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="ea5f4-112">Este artigo descreve como aplicativos toowrite que usam Olá SDK de Java do armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="ea5f4-113">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="ea5f4-113">Create a Java application</span></span>
<span data-ttu-id="ea5f4-114">exemplos de saudação toobuild, será necessário hello Java Development Kit (JDK) e [Olá [SDK do armazenamento do Azure para Java]].</span><span class="sxs-lookup"><span data-stu-id="ea5f4-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="ea5f4-115">Você também deverá ter criado uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="ea5f4-116">Configurar seu aplicativo toouse armazenamento de arquivo do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="ea5f4-117">Olá toouse APIs, o armazenamento do Azure adicionar Olá superior de toohello instrução saudação do arquivo de Java em que você pretende tooaccess serviço de armazenamento de saudação da seguir.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="ea5f4-118">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="ea5f4-119">toouse armazenamento de arquivo do Azure, você precisa de conta de armazenamento do Azure de tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ea5f4-120">Olá primeira etapa seria tooconfigure uma cadeia de caracteres de conexão que vamos usar conta de armazenamento do tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="ea5f4-121">Vamos definir uma toodo variável estática que.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="ea5f4-122">Substitua your_storage_account_name e your_storage_account_key por valores reais de saudação para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="ea5f4-123">Conectar-se a conta de armazenamento do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="ea5f4-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="ea5f4-124">conta de armazenamento do tooconnect tooyour, você precisa Olá toouse **CloudStorageAccount** um tooits de cadeia de caracteres de conexão de passagem do objeto **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="ea5f4-125">**CloudStorageAccount.parse** gera um InvalidKeyException, portanto, você precisará tooput dentro de um bloco try/catch bloquear.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="ea5f4-126">Criar um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-126">Create an Azure File share</span></span>
<span data-ttu-id="ea5f4-127">Todos os arquivos e diretórios do Armazenamento de Arquivos do Azure residem em um contêiner chamado **Compartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="ea5f4-128">Sua conta de armazenamento pode ter tantos compartilhamentos quantos a capacidade da conta permitir.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="ea5f4-129">compartilhamento de tooa tooobtain acesso e seu conteúdo, você precisa toouse um cliente de armazenamento do arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="ea5f4-130">Usando o cliente de armazenamento do Azure arquivo hello, em seguida, você pode obter um compartilhamento de tooa de referência.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="ea5f4-131">tooactually criar compartilhamento de hello, use Olá **createIfNotExists** método do objeto de CloudFileShare hello.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="ea5f4-132">Neste ponto, **compartilhar** contém um compartilhamento de tooa de referência chamado **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="ea5f4-133">Excluir um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-133">Delete an Azure File share</span></span>
<span data-ttu-id="ea5f4-134">Excluir um compartilhamento é feito através da chamada hello **deleteIfExists** método em um objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="ea5f4-135">O código fornecido a seguir é um exemplo de como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="ea5f4-136">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="ea5f4-136">Create a directory</span></span>
<span data-ttu-id="ea5f4-137">Você também pode organizar o armazenamento, colocando arquivos nos subdiretórios em vez de ter todos eles no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="ea5f4-138">Armazenamento de arquivo do Azure permite toocreate como permitem muito diretórios como será sua conta.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="ea5f4-139">saudação de código abaixo cria um subdiretório chamado **sampledir** no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="ea5f4-140">Excluir um diretório</span><span class="sxs-lookup"><span data-stu-id="ea5f4-140">Delete a directory</span></span>
<span data-ttu-id="ea5f4-141">Excluir um diretório é uma tarefa bem simples, embora deva-se observar que não é possível excluir um diretório que ainda contenha arquivos ou outros diretórios.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="ea5f4-142">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="ea5f4-143">A lista de arquivos e diretórios em um compartilhamento pode ser obtida facilmente chamando **listFilesAndDirectories** em uma referência CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="ea5f4-144">método Hello retorna uma lista de objetos ListFileItem que você pode iterar em.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="ea5f4-145">Por exemplo, hello código a seguir lista arquivos e diretórios dentro do diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="ea5f4-146">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="ea5f4-146">Upload a file</span></span>
<span data-ttu-id="ea5f4-147">Um arquivo Azure compartilhamento contém em Olá muito menos, um diretório raiz onde os arquivos podem residir.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="ea5f4-148">Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="ea5f4-149">a primeira etapa Olá no carregamento de um arquivo é tooobtain um diretório de toohello de referência em que ele deve residir.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="ea5f4-150">Para fazer isso, Olá chamada **getRootDirectoryReference** método do objeto de compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="ea5f4-151">Agora que você tem um diretório de raiz de toohello de referência do compartilhamento hello, você pode carregar um arquivo nele usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="ea5f4-152">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="ea5f4-152">Download a file</span></span>
<span data-ttu-id="ea5f4-153">Uma saudação mais frequentam operações que serão executadas em relação ao armazenamento de arquivo do Azure é arquivos toodownload.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="ea5f4-154">No hello exemplo a seguir, o código de saudação downloads SampleFile.txt e exibe seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="ea5f4-155">Excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="ea5f4-155">Delete a file</span></span>
<span data-ttu-id="ea5f4-156">Outra operação comum do Armazenamento de Arquivos do Azure é a exclusão de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="ea5f4-157">Olá, código a seguir exclui um arquivo chamado SampleFile.txt armazenados dentro de um diretório chamado **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="ea5f4-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea5f4-158">Next steps</span></span>
<span data-ttu-id="ea5f4-159">Se você quiser toolearn mais sobre outros APIs de armazenamento do Azure, siga estes links.</span><span class="sxs-lookup"><span data-stu-id="ea5f4-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="ea5f4-160">Central de Desenvolvedores do Java</span><span class="sxs-lookup"><span data-stu-id="ea5f4-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="ea5f4-161">SDK de Armazenamento do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="ea5f4-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="ea5f4-162">SDK de Armazenamento do Azure para Android</span><span class="sxs-lookup"><span data-stu-id="ea5f4-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="ea5f4-163">Referência de SDK do Cliente de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="ea5f4-164">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="ea5f4-165">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ea5f4-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="ea5f4-166">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="ea5f4-166">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
