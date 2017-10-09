---
title: aaaHow toouse o armazenamento de BLOBs do Azure (armazenamento de objeto) do Java | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="e5fa6-103">Como toouse armazenamento de Blob do Java</span><span class="sxs-lookup"><span data-stu-id="e5fa6-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="e5fa6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e5fa6-104">Overview</span></span>
<span data-ttu-id="e5fa6-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="e5fa6-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="e5fa6-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="e5fa6-108">Este artigo mostra como tooperform cenários comuns usando Olá armazenamento de BLOBs do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="e5fa6-109">exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="e5fa6-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="e5fa6-110">Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="e5fa6-111">Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#Next-Steps) seção.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="e5fa6-112">Um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="e5fa6-113">Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="e5fa6-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="e5fa6-114">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="e5fa6-114">Create a Java application</span></span>
<span data-ttu-id="e5fa6-115">Neste artigo, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="e5fa6-116">toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="e5fa6-117">Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="e5fa6-118">Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="e5fa6-119">Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="e5fa6-120">Configurar seu aplicativo tooaccess armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="e5fa6-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="e5fa6-121">Adicione Olá após a importação instruções toohello superior do arquivo de Java Olá onde você deseja que os blobs de tooaccess toouse Olá APIs de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e5fa6-122">Configurar uma cadeia de conexão de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e5fa6-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="e5fa6-123">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e5fa6-124">Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e5fa6-125">Olá exemplo a seguir mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="e5fa6-126">Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="e5fa6-127">Olá, exemplo a seguir obtém Olá cadeia de caracteres de conexão de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="e5fa6-128">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="e5fa6-129">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="e5fa6-129">Create a container</span></span>
<span data-ttu-id="e5fa6-130">Um objeto **CloudBlobClient** permite que você obtenha os objetos de referência para os contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="e5fa6-131">Olá código a seguir cria um **CloudBlobClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="e5fa6-132">Existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK do cliente de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="e5fa6-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="e5fa6-133">Saudação de uso **CloudBlobClient** tooget um contêiner de toohello de referência que você deseja toouse do objeto.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="e5fa6-134">Você pode criar o contêiner de saudação se ele não existir com hello **createIfNotExists** método, caso contrário, retornará o contêiner existente hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="e5fa6-135">Por padrão, novo contêiner de saudação é privado, portanto, você deve especificar sua chave de acesso de armazenamento (como feito anteriormente) blobs toodownload desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="e5fa6-136">Opcional: configurar um contêiner para acesso público</span><span class="sxs-lookup"><span data-stu-id="e5fa6-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="e5fa6-137">Permissões do contêiner são configuradas para acesso privado por padrão, mas você pode facilmente configurar permissões tooallow pública, somente leitura acesso um contêiner para todos os usuários em Olá Internet:</span><span class="sxs-lookup"><span data-stu-id="e5fa6-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e5fa6-138">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="e5fa6-138">Upload a blob into a container</span></span>
<span data-ttu-id="e5fa6-139">tooupload um blob de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="e5fa6-140">Quando você tem uma referência de blob, você pode carregar qualquer fluxo chamando o carregamento em referência de blob hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="e5fa6-141">Esta operação criará blob Olá se ele não existe ou substituí-lo se ele faz.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="e5fa6-142">saudação de exemplo de código a seguir mostra esse e supõe que esse contêiner Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="e5fa6-143">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="e5fa6-143">List hello blobs in a container</span></span>
<span data-ttu-id="e5fa6-144">blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner como você fez tooupload um blob.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="e5fa6-145">Você pode usar o contêiner de saudação **listBlobs** método com um **para** loop.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="e5fa6-146">Olá código a seguir gera Olá Uri de cada blob em um console de toohello do contêiner.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="e5fa6-147">Lembre-se de que você pode nomear blobs com informações de caminho em seus nomes.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="e5fa6-148">Isso cria uma estrutura de diretório virtual que você pode organizar e percorrer como faria com um sistema de arquivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="e5fa6-149">Observe que a estrutura de diretórios Olá só é virtual - Olá somente os recursos disponíveis no armazenamento de Blob são contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="e5fa6-150">No entanto, a biblioteca de saudação do cliente oferece uma **CloudBlobDirectory** objeto de diretório virtual do toorefer tooa e simplificar o processo de saudação do trabalho com blobs são organizados dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="e5fa6-151">Por exemplo, você pode ter um contêiner denominado “photos”, no qual poderia carregar os blobs “rootphoto1”, “2010/photo1”, “2010/photo2” e “2011/photo1”.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="e5fa6-152">Isso criaria Olá diretórios virtuais dentro do contêiner do "fotos" hello "2011" e "2010".</span><span class="sxs-lookup"><span data-stu-id="e5fa6-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="e5fa6-153">Quando você chama **listBlobs** no contêiner do "fotos" Olá, coleção Olá retornada conterá **CloudBlobDirectory** e **CloudBlob** objetos que representam Olá diretórios e blobs presentes no nível superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="e5fa6-154">Nesse caso, os diretórios “2010” e “2011”, bem como “rootphoto1” de photo, seriam retornados.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="e5fa6-155">Você pode usar o hello **instanceof** toodistinguish operador esses objetos.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="e5fa6-156">Opcionalmente, você pode passar parâmetros toohello **listBlobs** método com hello **useFlatBlobListing** parâmetro definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="e5fa6-157">Isso resultará no retorno de cada blob, independentemente do diretório.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="e5fa6-158">Para obter mais informações, consulte **Cloudblobcontainer** em Olá [referência de SDK do cliente de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="e5fa6-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="e5fa6-159">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="e5fa6-159">Download a blob</span></span>
<span data-ttu-id="e5fa6-160">blobs toodownload, siga Olá mesmo as etapas de como você fez para carregar um blob em ordem tooget uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="e5fa6-161">Em Olá carregamento de exemplo, você chamou o carregamento no objeto de blob hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="e5fa6-162">Olá exemplo a seguir, chamar download tootransfer Olá conteúdo tooa fluxo objeto blob como um **FileOutputStream** que você pode usar o arquivo do local de tooa toopersist Olá blob.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="e5fa6-163">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="e5fa6-163">Delete a blob</span></span>
<span data-ttu-id="e5fa6-164">toodelete um blob, obter um blob de referência e, em seguida, chamar **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="e5fa6-165">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="e5fa6-165">Delete a blob container</span></span>
<span data-ttu-id="e5fa6-166">Por fim, toodelete um contêiner de blob, obter um blob de referência de contêiner e chame **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="e5fa6-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5fa6-167">Next steps</span></span>
<span data-ttu-id="e5fa6-168">Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5fa6-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="e5fa6-169">[Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)</span><span class="sxs-lookup"><span data-stu-id="e5fa6-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="e5fa6-170">[referência de SDK do cliente de armazenamento do Azure][referência de SDK do cliente de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="e5fa6-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="e5fa6-171">[Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="e5fa6-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="e5fa6-172">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="e5fa6-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="e5fa6-173">Para obter mais informações, consulte também Olá [Central de desenvolvedores de Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="e5fa6-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK do cliente de armazenamento do Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
