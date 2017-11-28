---
title: Como usar o Armazenamento de Blobs do Azure (armazenamento de objeto) do Java | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: b8a4eca600b458802a7a23851bb80ea4da2664ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="5d366-103">Como usar o Armazenamento de Blob do Java</span><span class="sxs-lookup"><span data-stu-id="5d366-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="5d366-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5d366-104">Overview</span></span>
<span data-ttu-id="5d366-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="5d366-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="5d366-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d366-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5d366-107">O Armazenamento de Blobs também é chamado de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="5d366-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="5d366-108">Este artigo mostra como executar cenários comuns usando o armazenamento de Blob do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5d366-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="5d366-109">As amostras são escritas em Java e usam o [SDK de Armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5d366-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="5d366-110">Os cenários abrangidos incluem **carregamento**, **listagem**, **download** e **exclusão** de blobs.</span><span class="sxs-lookup"><span data-stu-id="5d366-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="5d366-111">Para obter mais informações sobre blobs, consulte a seção [Próximas etapas](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="5d366-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="5d366-112">Um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="5d366-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="5d366-113">Para obter mais informações, consulte [Azure Storage SDK for Android][Azure Storage SDK for Android] (SDK de Armazenamento do Azure para Android).</span><span class="sxs-lookup"><span data-stu-id="5d366-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="5d366-114">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="5d366-114">Create a Java application</span></span>
<span data-ttu-id="5d366-115">Neste artigo, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d366-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="5d366-116">Para isso, você precisará instalar o JDK (Java Development Kit) e criar uma conta de armazenamento do Azure na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d366-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="5d366-117">Depois disso, você precisará verificar se o sistema de desenvolvimento atende aos requisitos mínimos e às dependências listadas no repositório [Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d366-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="5d366-118">Se o seu sistema atender a esses requisitos, você poderá seguir as instruções para baixar e instalar as Bibliotecas de Armazenamento do Azure para Java em seu sistema por meio desse repositório.</span><span class="sxs-lookup"><span data-stu-id="5d366-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="5d366-119">Depois de concluir essas tarefas, você poderá criar um aplicativo Java que usa os exemplos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5d366-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="5d366-120">Configurar seu aplicativo para acessar o armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="5d366-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="5d366-121">Adicione as seguintes instruções de importação à parte superior do arquivo Java no qual deseja usar as APIs de Armazenamento do Azure para acessar blobs.</span><span class="sxs-lookup"><span data-stu-id="5d366-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="5d366-122">Configurar uma cadeia de conexão de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5d366-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="5d366-123">Um cliente de Armazenamento do Azure usa uma cadeia de conexão para armazenar pontos de extremidade e credenciais para acessar serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="5d366-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="5d366-124">Ao executar um aplicativo cliente, é necessário fornecer a cadeia de conexão de armazenamento no formato a seguir, usando o nome de sua conta de armazenamento e a tecla de Acesso primário da conta de armazenamento listada no [portal do Azure](https://portal.azure.com) para os valores *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="5d366-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="5d366-125">O exemplo a seguir mostra como é possível declarar um campo estático para armazenar a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="5d366-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="5d366-126">Em um aplicativo que esteja sendo executado em uma função no Microsoft Azure, essa cadeia pode ser armazenada no arquivo de configuração do serviço, *ServiceConfiguration.cscfg*, podendo ser acessada com uma chamada para o método **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="5d366-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="5d366-127">O exemplo a seguir obtém a cadeia de conexão de um elemento **Setting** chamado *StorageConnectionString* no arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="5d366-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="5d366-128">Os exemplos abaixo pressupõem que você usou um desses dois métodos para obter a cadeia de conexão do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5d366-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="5d366-129">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="5d366-129">Create a container</span></span>
<span data-ttu-id="5d366-130">Um objeto **CloudBlobClient** permite que você obtenha os objetos de referência para os contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="5d366-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="5d366-131">O código a seguir cria um objeto **CloudBlobClient** .</span><span class="sxs-lookup"><span data-stu-id="5d366-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="5d366-132">Existem outras maneiras de criar objetos **CloudStorageAccount**. Para obter mais informações, confira **CloudStorageAccount** na [Referência de SDK do cliente de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="5d366-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5d366-133">Use o objeto **CloudBlobClient** para obter uma referência ao contêiner que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="5d366-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="5d366-134">Se o contêiner não existir, será possível criá-lo com o método **createIfNotExists** ; caso contrário, ele retornará o contêiner existente.</span><span class="sxs-lookup"><span data-stu-id="5d366-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="5d366-135">Por padrão, o novo contêiner é particular; portanto, você deve especificar sua chave de acesso de armazenamento (como anteriormente) para baixar blobs desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="5d366-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="5d366-136">Opcional: configurar um contêiner para acesso público</span><span class="sxs-lookup"><span data-stu-id="5d366-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="5d366-137">Por padrão, as permissões de um contêiner são configuradas para acesso privado, mas você pode configurar facilmente as permissões de um contêiner para permitir acesso público somente leitura a todos os usuários na Internet:</span><span class="sxs-lookup"><span data-stu-id="5d366-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5d366-138">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="5d366-138">Upload a blob into a container</span></span>
<span data-ttu-id="5d366-139">Para carregar um arquivo em um blob, obtenha uma referência de contêiner e use-a para obter uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="5d366-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="5d366-140">Depois de obter uma referência do blob, é possível carregar qualquer fluxo chamando o upload na referência de blob.</span><span class="sxs-lookup"><span data-stu-id="5d366-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="5d366-141">Essa operação criará o blob, se ele não existir, ou o substituirá, se ele já existir.</span><span class="sxs-lookup"><span data-stu-id="5d366-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="5d366-142">O exemplo de código a seguir mostra isso e pressupõe que o contêiner já foi criado.</span><span class="sxs-lookup"><span data-stu-id="5d366-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="5d366-143">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="5d366-143">List the blobs in a container</span></span>
<span data-ttu-id="5d366-144">Para listar os blobs em um contêiner, primeiro obtenha uma referência do contêiner como a que você obteve para carregar um blob.</span><span class="sxs-lookup"><span data-stu-id="5d366-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="5d366-145">É possível usar o método **listBlobs** do contêiner com um loop **for**.</span><span class="sxs-lookup"><span data-stu-id="5d366-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="5d366-146">O código a seguir gera a saída do Uri de cada blob em um contêiner para o console.</span><span class="sxs-lookup"><span data-stu-id="5d366-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="5d366-147">Lembre-se de que você pode nomear blobs com informações de caminho em seus nomes.</span><span class="sxs-lookup"><span data-stu-id="5d366-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="5d366-148">Isso cria uma estrutura de diretório virtual que você pode organizar e percorrer como faria com um sistema de arquivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="5d366-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="5d366-149">Observe que a estrutura do diretório é virtual apenas - os somente os recursos disponíveis no armazenamento de Blob são contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="5d366-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="5d366-150">No entanto, a biblioteca de cliente oferece um objeto **CloudBlobDirectory** para fazer referência a um diretório virtual e simplificar o processo de trabalhar com blobs que são organizados dessa forma.</span><span class="sxs-lookup"><span data-stu-id="5d366-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="5d366-151">Por exemplo, você pode ter um contêiner denominado “photos”, no qual poderia carregar os blobs “rootphoto1”, “2010/photo1”, “2010/photo2” e “2011/photo1”.</span><span class="sxs-lookup"><span data-stu-id="5d366-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="5d366-152">Isso criaria os diretórios virtuais "2010" e "2011" no contêiner “photos".</span><span class="sxs-lookup"><span data-stu-id="5d366-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="5d366-153">Quando você chamar **listBlobs** no contêiner "photos", a coleção retornada conterá os objetos **CloudBlobDirectory** e **CloudBlob** que representam os diretórios e os blobs contidos no nível superior.</span><span class="sxs-lookup"><span data-stu-id="5d366-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="5d366-154">Nesse caso, os diretórios “2010” e “2011”, bem como “rootphoto1” de photo, seriam retornados.</span><span class="sxs-lookup"><span data-stu-id="5d366-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="5d366-155">É possível usar o operador **instanceof** para distinguir esses objetos.</span><span class="sxs-lookup"><span data-stu-id="5d366-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="5d366-156">Como alternativa, você pode transmitir parâmetros para o método **listBlobs** com o parâmetro **useFlatBlobListing** definido como true.</span><span class="sxs-lookup"><span data-stu-id="5d366-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="5d366-157">Isso resultará no retorno de cada blob, independentemente do diretório.</span><span class="sxs-lookup"><span data-stu-id="5d366-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="5d366-158">Para obter mais informações, veja **CloudBlobContainer.listBlobs** na [Referência de SDK do cliente de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="5d366-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="5d366-159">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="5d366-159">Download a blob</span></span>
<span data-ttu-id="5d366-160">Para baixar blobs, siga as mesmas etapas utilizadas para carregar um blob, a fim de obter uma referência do blob.</span><span class="sxs-lookup"><span data-stu-id="5d366-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="5d366-161">No exemplo de carregamento, você chamou o carregamento no objeto do blob.</span><span class="sxs-lookup"><span data-stu-id="5d366-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="5d366-162">No exemplo a seguir, chame o download para transferir o conteúdo do blob para um objeto do fluxo, como um **FileOutputStream** que pode ser usado para persistir o blob ao arquivo local.</span><span class="sxs-lookup"><span data-stu-id="5d366-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="5d366-163">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="5d366-163">Delete a blob</span></span>
<span data-ttu-id="5d366-164">Para excluir um blob, obtenha uma referência do blob e chame **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="5d366-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="5d366-165">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="5d366-165">Delete a blob container</span></span>
<span data-ttu-id="5d366-166">Por fim, para excluir um contêiner de blob, obtenha uma referência do contêiner de blob e chame **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="5d366-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="5d366-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d366-167">Next steps</span></span>
<span data-ttu-id="5d366-168">Agora que você aprendeu os conceitos básicos do armazenamento de blob, siga estes links para saber mais sobre tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="5d366-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="5d366-169">[Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)</span><span class="sxs-lookup"><span data-stu-id="5d366-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="5d366-170">[Referência de SDK do cliente de armazenamento do Azure][Referência de SDK do cliente de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="5d366-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="5d366-171">[Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="5d366-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="5d366-172">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="5d366-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="5d366-173">Para obter mais informações, consulte também o [Centro de desenvolvedores do Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="5d366-173">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="5d366-174">[Referência de SDK do cliente de armazenamento do Azure]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="5d366-174">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
