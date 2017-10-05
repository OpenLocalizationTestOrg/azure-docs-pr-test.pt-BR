---
title: Desenvolvimento para o Armazenamento de Arquivos do Azure com Java | Microsoft Docs
description: "Saiba como desenvolver aplicativos e serviços Java que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo."
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
ms.openlocfilehash: 16924599e49990265e07f7a58613756d93c46942
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="4096c-103">Desenvolvimento para o Armazenamento de Arquivos do Azure com Java</span><span class="sxs-lookup"><span data-stu-id="4096c-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="4096c-104">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="4096c-104">About this tutorial</span></span>
<span data-ttu-id="4096c-105">Este tutorial demonstrará as noções básicas de usar Java para desenvolver aplicativos ou serviços que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo.</span><span class="sxs-lookup"><span data-stu-id="4096c-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="4096c-106">Neste tutorial, criaremos um aplicativo de console simples e mostraremos como executar ações básicas com Java e o Armazenamento de Arquivos do Azure:</span><span class="sxs-lookup"><span data-stu-id="4096c-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="4096c-107">Criar e excluir Compartilhamentos de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="4096c-108">Criar e excluir diretórios</span><span class="sxs-lookup"><span data-stu-id="4096c-108">Create and delete directories</span></span>
* <span data-ttu-id="4096c-109">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="4096c-110">Carregar, baixar e excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="4096c-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="4096c-111">Como o Armazenamento de Arquivos do Azure pode ser acessado via SMB, é possível criar aplicativos simples que acessam o Compartilhamento de Arquivos do Azure usando as classes padrão de E/S do Java.</span><span class="sxs-lookup"><span data-stu-id="4096c-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="4096c-112">Este artigo descreverá como criar aplicativos que usam o SDK do Java do Armazenamento do Azure, que usa a [API REST do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) para se comunicar com o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4096c-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="4096c-113">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="4096c-113">Create a Java application</span></span>
<span data-ttu-id="4096c-114">Para criar os exemplos, você precisará do JDK (Java Development Kit) e do [SDK do Armazenamento do Azure para Java][].</span><span class="sxs-lookup"><span data-stu-id="4096c-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="4096c-115">Você também deverá ter criado uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4096c-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="4096c-116">Configurar seu aplicativo para usar o Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="4096c-117">Para usar as APIs de armazenamento do Azure, adicione a instrução a seguir à parte superior do arquivo Java do qual você pretende acessar o serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="4096c-118">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="4096c-119">Para usar o Armazenamento de Arquivos do Azure, será necessário se conectar à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4096c-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="4096c-120">A primeira etapa seria configurar uma cadeia de conexão que usaremos para acessar a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="4096c-121">Vamos definir uma variável estática para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="4096c-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="4096c-122">Substitua nome_da_sua_conta_de_armazenamento e chave_da_sua_conta_de_armazenamento pelos valores reais da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="4096c-123">Conectar-se a uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="4096c-124">Para se conectar à sua conta de armazenamento, você precisa usar o objeto **CloudStorageAccount**, passando uma cadeia de conexão para seu método de **análise**.</span><span class="sxs-lookup"><span data-stu-id="4096c-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="4096c-125">**CloudStorageAccount.parse** gera uma InvalidKeyException; portanto, você precisará colocá-lo dentro de um bloco try/catch.</span><span class="sxs-lookup"><span data-stu-id="4096c-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="4096c-126">Criar um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-126">Create an Azure File share</span></span>
<span data-ttu-id="4096c-127">Todos os arquivos e diretórios do Armazenamento de Arquivos do Azure residem em um contêiner chamado **Compartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="4096c-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="4096c-128">Sua conta de armazenamento pode ter tantos compartilhamentos quantos a capacidade da conta permitir.</span><span class="sxs-lookup"><span data-stu-id="4096c-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="4096c-129">Para obter acesso a um compartilhamento e seu conteúdo, é necessário usar um cliente de Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4096c-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="4096c-130">Usando o cliente do Armazenamento de Arquivos do Azure, será possível obter uma referência a um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="4096c-131">Para realmente criar o compartilhamento, use o método **createIfNotExists** do objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="4096c-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="4096c-132">Neste ponto, **compartilhar** contém uma referência a um compartilhamento chamado **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="4096c-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="4096c-133">Excluir um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-133">Delete an Azure File share</span></span>
<span data-ttu-id="4096c-134">Para excluir um compartilhamento deve-se chamar o método **deleteIfExists** em um objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="4096c-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="4096c-135">O código fornecido a seguir é um exemplo de como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="4096c-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="4096c-136">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="4096c-136">Create a directory</span></span>
<span data-ttu-id="4096c-137">Você também pode organizar o armazenamento colocando arquivos em subdiretórios em vez de manter todos eles no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="4096c-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="4096c-138">O Armazenamento de Arquivos do Azure permite criar que você crie quantos diretórios a conta permitir.</span><span class="sxs-lookup"><span data-stu-id="4096c-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="4096c-139">O código a seguir criará um subdiretório chamado **sampledir** no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="4096c-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="4096c-140">Excluir um diretório</span><span class="sxs-lookup"><span data-stu-id="4096c-140">Delete a directory</span></span>
<span data-ttu-id="4096c-141">Excluir um diretório é uma tarefa bem simples, embora deva-se observar que não é possível excluir um diretório que ainda contenha arquivos ou outros diretórios.</span><span class="sxs-lookup"><span data-stu-id="4096c-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="4096c-142">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="4096c-143">A lista de arquivos e diretórios em um compartilhamento pode ser obtida facilmente chamando **listFilesAndDirectories** em uma referência CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="4096c-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="4096c-144">O método retorna uma lista de objetos ListFileItem nos quais você pode iterar.</span><span class="sxs-lookup"><span data-stu-id="4096c-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="4096c-145">Como exemplo, o código a seguir lista os arquivos e diretórios contidos no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="4096c-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="4096c-146">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="4096c-146">Upload a file</span></span>
<span data-ttu-id="4096c-147">Um compartilhamento de Arquivos do Azure contém, no mínimo, um diretório raiz em que os arquivos podem residir.</span><span class="sxs-lookup"><span data-stu-id="4096c-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="4096c-148">Nesta seção, você aprenderá a carregar um arquivo do armazenamento local para o diretório raiz de um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="4096c-149">A primeira etapa do carregamento de um arquivo é obter uma referência para o diretório onde ele deve residir.</span><span class="sxs-lookup"><span data-stu-id="4096c-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="4096c-150">Para isso, você deve chamar o método **getRootDirectoryReference** do objeto de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4096c-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="4096c-151">Agora que você tem uma referência para o diretório raiz do compartilhamento, pode carregar um arquivo usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="4096c-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="4096c-152">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="4096c-152">Download a file</span></span>
<span data-ttu-id="4096c-153">Uma das operações mais frequentes executadas no Armazenamento de Arquivos do Azure é baixar arquivos.</span><span class="sxs-lookup"><span data-stu-id="4096c-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="4096c-154">No exemplo a seguir, o código baixa o arquivo SampleFile.txt e exibe seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4096c-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="4096c-155">Excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="4096c-155">Delete a file</span></span>
<span data-ttu-id="4096c-156">Outra operação comum do Armazenamento de Arquivos do Azure é a exclusão de arquivos.</span><span class="sxs-lookup"><span data-stu-id="4096c-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="4096c-157">O código a seguir exclui um arquivo chamado SampleFile.txt armazenado em um diretório chamado **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="4096c-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="4096c-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4096c-158">Next steps</span></span>
<span data-ttu-id="4096c-159">Se você quiser saber mais sobre outras APIs de armazenamento do Azure, siga estes links.</span><span class="sxs-lookup"><span data-stu-id="4096c-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="4096c-160">Central de Desenvolvedores do Java</span><span class="sxs-lookup"><span data-stu-id="4096c-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="4096c-161">SDK de Armazenamento do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="4096c-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="4096c-162">SDK de Armazenamento do Azure para Android</span><span class="sxs-lookup"><span data-stu-id="4096c-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="4096c-163">Referência de SDK do Cliente de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="4096c-164">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="4096c-165">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4096c-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="4096c-166">Transferir dados com o Utilitário de Linha de Comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="4096c-166">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)