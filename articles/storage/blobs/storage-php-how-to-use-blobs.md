---
title: Como usar o armazenamento de blobs (armazenamento de objeto) do PHP | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4b68844c5d0553eaede3997bf09bff4fe570e850
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="d5da5-103">Como usar o armazenamento de blob no PHP</span><span class="sxs-lookup"><span data-stu-id="d5da5-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d5da5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d5da5-104">Overview</span></span>
<span data-ttu-id="d5da5-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="d5da5-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="d5da5-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5da5-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="d5da5-107">O Armazenamento de Blobs também é chamado de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="d5da5-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="d5da5-108">Este guia mostrará como executar cenários comuns usando o serviço Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5da5-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="d5da5-109">As amostras são escritas em PHP e usam o [SDK do Azure para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="d5da5-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="d5da5-110">Os cenários abrangidos incluem **carregamento**, **listagem**, **download** e **exclusão** de blobs.</span><span class="sxs-lookup"><span data-stu-id="d5da5-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="d5da5-111">Para saber mais sobre blobs, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="d5da5-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="d5da5-112">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="d5da5-112">Create a PHP application</span></span>
<span data-ttu-id="d5da5-113">O único requisito para a criação de um aplicativo PHP que acessa o serviço Blob do Azure é a referência de classes no SDK do Azure para PHP em seu código.</span><span class="sxs-lookup"><span data-stu-id="d5da5-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="d5da5-114">Você pode usar as ferramentas de desenvolvimento para criar seu aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="d5da5-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="d5da5-115">Neste guia, você usará os recursos de serviços que podem ser chamados em um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, uma função de trabalho ou um site.</span><span class="sxs-lookup"><span data-stu-id="d5da5-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="d5da5-116">Obter as bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="d5da5-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="d5da5-117">Configurar seu aplicativo para acessar o serviço Blob</span><span class="sxs-lookup"><span data-stu-id="d5da5-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="d5da5-118">Para usar as APIs do serviço Blob do Azure, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d5da5-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="d5da5-119">Fazer referência ao arquivo de carregador automático usando a instrução [require_once], e</span><span class="sxs-lookup"><span data-stu-id="d5da5-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="d5da5-120">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="d5da5-120">Reference any classes you might use.</span></span>

<span data-ttu-id="d5da5-121">O exemplo a seguir mostra como incluir o arquivo de carregador automático e fazer referência à classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="d5da5-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="d5da5-122">Os exemplos deste artigo pressupõem que você tenha instalado as Bibliotecas de Cliente do PHP para o Azure por meio do Criador.</span><span class="sxs-lookup"><span data-stu-id="d5da5-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="d5da5-123">Se tiver instalado as bibliotecas manualmente, você precisará fazer referência ao arquivo de carregador automático `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="d5da5-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="d5da5-124">Nos exemplos abaixo, a instrução `require_once` será mostrada sempre, mas somente as classes necessárias para executar o exemplo serão referenciadas.</span><span class="sxs-lookup"><span data-stu-id="d5da5-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d5da5-125">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d5da5-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="d5da5-126">Para criar uma instância de um cliente de serviço Blob do Azure, você deve primeiramente ter uma cadeia de conexão válida.</span><span class="sxs-lookup"><span data-stu-id="d5da5-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="d5da5-127">O formato da cadeia de conexão do serviço blob é:</span><span class="sxs-lookup"><span data-stu-id="d5da5-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="d5da5-128">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="d5da5-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="d5da5-129">Para acessar o emulador de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="d5da5-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="d5da5-130">Para criar qualquer cliente de serviço do Azure, é necessário usar a classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="d5da5-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="d5da5-131">Você pode:</span><span class="sxs-lookup"><span data-stu-id="d5da5-131">You can:</span></span>

* <span data-ttu-id="d5da5-132">Passar a cadeia de conexão diretamente para ele ou</span><span class="sxs-lookup"><span data-stu-id="d5da5-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="d5da5-133">Usar **CloudConfigurationManager (CCM)** para verificar várias fontes externas da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="d5da5-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="d5da5-134">Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="d5da5-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="d5da5-135">É possível adicionar novas origens ao estender a classe **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="d5da5-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="d5da5-136">Para os exemplos descritos aqui, a cadeia de conexão será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="d5da5-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="d5da5-137">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="d5da5-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d5da5-138">O objeto **BlobRestProxy** permite que você crie um contêiner de blob com o método **createContainer**.</span><span class="sxs-lookup"><span data-stu-id="d5da5-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="d5da5-139">Ao criar um contêiner, você pode definir opções no contêiner, mas fazer isso não é necessário.</span><span class="sxs-lookup"><span data-stu-id="d5da5-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="d5da5-140">(O exemplo a seguir mostra como definir os metadados do contêiner e a ACL [lista de controle de acesso] do contêiner.)</span><span class="sxs-lookup"><span data-stu-id="d5da5-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="d5da5-141">A chamada a **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** tornam os dados do contêiner e do blob acessíveis por meio de solicitações anônimas.</span><span class="sxs-lookup"><span data-stu-id="d5da5-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="d5da5-142">A chamada a **setPublicAccess(PublicAccessType::BLOBS_ONLY)** tornam apenas os dados do blob acessíveis por meio de solicitações anônimas.</span><span class="sxs-lookup"><span data-stu-id="d5da5-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="d5da5-143">Para obter mais informações sobre as ACLs do contêiner, consulte [Set Container ACL (REST API)][container-acl] (Definir a ACL do contêiner [API REST]).</span><span class="sxs-lookup"><span data-stu-id="d5da5-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="d5da5-144">Para obter mais informações sobre os códigos de erro do serviço Blob, consulte [Blob Service Error Codes][error-codes] (Códigos de erro do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="d5da5-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d5da5-145">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="d5da5-145">Upload a blob into a container</span></span>
<span data-ttu-id="d5da5-146">Para carregar um arquivo como um blob, use o método **BlobRestProxy->createBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="d5da5-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="d5da5-147">Essa operação cria o blob, se ele não existir, ou o substitui, se ele já existir.</span><span class="sxs-lookup"><span data-stu-id="d5da5-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="d5da5-148">O exemplo de código abaixo pressupõe que o contêiner já foi criado e usa [fopen][fopen] para abrir o arquivo como uma transmissão.</span><span class="sxs-lookup"><span data-stu-id="d5da5-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="d5da5-149">Observe que o exemplo anterior carrega um blob como um fluxo.</span><span class="sxs-lookup"><span data-stu-id="d5da5-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="d5da5-150">No entanto, um blob também pode ser carregado como uma cadeia de caracteres usando, por exemplo, a função [file\_get\_contents][file_get_contents].</span><span class="sxs-lookup"><span data-stu-id="d5da5-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="d5da5-151">Para fazer isso usando o exemplo anterior, altere `$content = fopen("c:\myfile.txt", "r");` para `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="d5da5-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d5da5-152">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="d5da5-152">List the blobs in a container</span></span>
<span data-ttu-id="d5da5-153">Para listar os blobs em um contêiner, use o método **BlobRestProxy->listBlobs** com um loop **foreach** para executar um loop pelo resultado.</span><span class="sxs-lookup"><span data-stu-id="d5da5-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="d5da5-154">O código a seguir mostra o nome de cada blob como resultado em um contêiner e exibe seu URI para o navegador.</span><span class="sxs-lookup"><span data-stu-id="d5da5-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="d5da5-155">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="d5da5-155">Download a blob</span></span>
<span data-ttu-id="d5da5-156">Para baixar um blob, chame o método **BlobRestProxy->getBlob** e, em seguida, chame o método **getContentStream** no objeto **GetBlobResult** resultante.</span><span class="sxs-lookup"><span data-stu-id="d5da5-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="d5da5-157">Observe que o exemplo acima obtém um blob como um recurso de fluxo (o comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="d5da5-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="d5da5-158">No entanto, é possível usar a função [stream\_get\_contents][stream-get-contents] para converter a transmissão retornada em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d5da5-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d5da5-159">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="d5da5-159">Delete a blob</span></span>
<span data-ttu-id="d5da5-160">Para excluir um blob, passe o nome do contêiner e o nome do blob para **BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="d5da5-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="d5da5-161">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="d5da5-161">Delete a blob container</span></span>
<span data-ttu-id="d5da5-162">Por fim, para excluir um contêiner de blob, passe o nome do contêiner para **BlobRestProxy->deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="d5da5-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="d5da5-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5da5-163">Next steps</span></span>
<span data-ttu-id="d5da5-164">Agora que você aprendeu os conceitos básicos do serviço Blob do Azure, siga estes links para saber mais sobre tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="d5da5-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="d5da5-165">Visite o [Blog da Equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="d5da5-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="d5da5-166">Confira o [exemplo de blob de blocos PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="d5da5-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="d5da5-167">Confira o [exemplo de blob de páginas PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="d5da5-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="d5da5-168">Transferir dados com o Utilitário de Linha de Comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="d5da5-168">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="d5da5-169">Para saber mais, veja também a [Central de desenvolvedores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d5da5-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
