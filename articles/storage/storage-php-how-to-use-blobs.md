---
title: armazenamento de blob aaaHow toouse (armazenamento de objeto) do PHP | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="6bd51-103">Como toouse blob storage do PHP</span><span class="sxs-lookup"><span data-stu-id="6bd51-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6bd51-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6bd51-104">Overview</span></span>
<span data-ttu-id="6bd51-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="6bd51-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="6bd51-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6bd51-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="6bd51-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="6bd51-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="6bd51-108">Este guia mostra como os cenários comuns de tooperform usando hello Azure serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="6bd51-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="6bd51-109">exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="6bd51-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="6bd51-110">Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs.</span><span class="sxs-lookup"><span data-stu-id="6bd51-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="6bd51-111">Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="6bd51-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="6bd51-112">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="6bd51-112">Create a PHP application</span></span>
<span data-ttu-id="6bd51-113">Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de blob do Azure Olá Olá referência de classes hello Azure SDK para PHP de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="6bd51-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="6bd51-114">Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="6bd51-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="6bd51-115">Neste guia, você usará os recursos de serviços que podem ser chamados em um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, uma função de trabalho ou um site.</span><span class="sxs-lookup"><span data-stu-id="6bd51-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="6bd51-116">Obter bibliotecas de saudação do cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="6bd51-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="6bd51-117">Configurar o serviço de blob do aplicativo tooaccess Olá</span><span class="sxs-lookup"><span data-stu-id="6bd51-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="6bd51-118">toouse hello Azure APIs do serviço blob, você precisa:</span><span class="sxs-lookup"><span data-stu-id="6bd51-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="6bd51-119">Arquivo de carregador automático de saudação de referência usando Olá [require_once] instrução, e</span><span class="sxs-lookup"><span data-stu-id="6bd51-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="6bd51-120">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="6bd51-120">Reference any classes you might use.</span></span>

<span data-ttu-id="6bd51-121">Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="6bd51-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd51-122">exemplos de Olá neste artigo presumem que você instalou Olá bibliotecas de cliente do PHP para o Azure por meio do criador.</span><span class="sxs-lookup"><span data-stu-id="6bd51-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="6bd51-123">Se você instalou bibliotecas Olá manualmente, você precisa Olá tooreference `WindowsAzure.php` arquivo do carregador automático.</span><span class="sxs-lookup"><span data-stu-id="6bd51-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="6bd51-124">Nos exemplos de saudação abaixo, Olá `require_once` instrução serão sempre mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="6bd51-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="6bd51-125">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6bd51-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="6bd51-126">tooinstantiate um cliente do serviço blob do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido.</span><span class="sxs-lookup"><span data-stu-id="6bd51-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="6bd51-127">cadeia de conexão de serviço de blob Olá Olá formato é:</span><span class="sxs-lookup"><span data-stu-id="6bd51-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="6bd51-128">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="6bd51-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="6bd51-129">Para acessar o emulador de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="6bd51-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="6bd51-130">toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="6bd51-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="6bd51-131">Você pode:</span><span class="sxs-lookup"><span data-stu-id="6bd51-131">You can:</span></span>

* <span data-ttu-id="6bd51-132">passar conexão Olá tooit cadeia de caracteres diretamente ou</span><span class="sxs-lookup"><span data-stu-id="6bd51-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="6bd51-133">Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="6bd51-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="6bd51-134">Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="6bd51-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="6bd51-135">Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="6bd51-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="6bd51-136">Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="6bd51-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="6bd51-137">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="6bd51-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="6bd51-138">Um **BlobRestProxy** objeto permite que você crie um contêiner de blob com hello **createContainer** método.</span><span class="sxs-lookup"><span data-stu-id="6bd51-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="6bd51-139">Ao criar um contêiner, você pode definir opções no contêiner hello, mas fazer isso não é necessário.</span><span class="sxs-lookup"><span data-stu-id="6bd51-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="6bd51-140">(o exemplo hello abaixo mostra como contêiner de saudação tooset acesso (ACL) da lista de controle e os metadados do contêiner.)</span><span class="sxs-lookup"><span data-stu-id="6bd51-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="6bd51-141">Chamando **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOBS)** torna Olá contêiner e blob de dados acessíveis via solicitações anônimas.</span><span class="sxs-lookup"><span data-stu-id="6bd51-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="6bd51-142">A chamada a **setPublicAccess(PublicAccessType::BLOBS_ONLY)** tornam apenas os dados do blob acessíveis por meio de solicitações anônimas.</span><span class="sxs-lookup"><span data-stu-id="6bd51-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="6bd51-143">Para obter mais informações sobre as ACLs do contêiner, consulte [Set Container ACL (REST API)][container-acl] (Definir a ACL do contêiner [API REST]).</span><span class="sxs-lookup"><span data-stu-id="6bd51-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="6bd51-144">Para obter mais informações sobre os códigos de erro do serviço Blob, consulte [Blob Service Error Codes][error-codes] (Códigos de erro do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="6bd51-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6bd51-145">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="6bd51-145">Upload a blob into a container</span></span>
<span data-ttu-id="6bd51-146">tooupload um arquivo como um blob, use Olá **BlobRestProxy -> createBlockBlob** método.</span><span class="sxs-lookup"><span data-stu-id="6bd51-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="6bd51-147">Essa operação cria blob Olá se ele não existe ou substitui-lo se ele faz.</span><span class="sxs-lookup"><span data-stu-id="6bd51-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="6bd51-148">Hello exemplo de código a seguir supõe que esse contêiner Olá já foi criado e usa [fopen] [ fopen] tooopen arquivo de saudação como um fluxo.</span><span class="sxs-lookup"><span data-stu-id="6bd51-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="6bd51-149">Observe que o exemplo anterior de Olá carrega um blob como um fluxo.</span><span class="sxs-lookup"><span data-stu-id="6bd51-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="6bd51-150">No entanto, um blob também pode ser carregado como uma cadeia de caracteres usando, por exemplo, Olá [arquivo\_obter\_conteúdo] [ file_get_contents] função.</span><span class="sxs-lookup"><span data-stu-id="6bd51-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="6bd51-151">toodo este usando o exemplo anterior hello, altere `$content = fopen("c:\myfile.txt", "r");` muito`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="6bd51-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="6bd51-152">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="6bd51-152">List hello blobs in a container</span></span>
<span data-ttu-id="6bd51-153">blobs de saudação toolist em um contêiner, use Olá **BlobRestProxy -> listBlobs** método com um **foreach** tooloop por meio do resultado de saudação de loop.</span><span class="sxs-lookup"><span data-stu-id="6bd51-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="6bd51-154">Olá código a seguir exibe o nome de saudação de cada blob como a saída em um contêiner e exibe seu navegador de toohello do URI.</span><span class="sxs-lookup"><span data-stu-id="6bd51-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="6bd51-155">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="6bd51-155">Download a blob</span></span>
<span data-ttu-id="6bd51-156">toodownload um blob, chamada hello **BlobRestProxy -> getBlob** método, então a saudação da chamada **getContentStream** método hello resultante **GetBlobResult** objeto.</span><span class="sxs-lookup"><span data-stu-id="6bd51-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="6bd51-157">Observe que esse exemplo hello acima obtém um blob como um recurso de fluxo (comportamento padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="6bd51-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="6bd51-158">No entanto, você pode usar o hello [fluxo\_obter\_conteúdo] [ stream-get-contents] saudação do função tooconvert retornou uma cadeia tooa fluxo.</span><span class="sxs-lookup"><span data-stu-id="6bd51-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="6bd51-159">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="6bd51-159">Delete a blob</span></span>
<span data-ttu-id="6bd51-160">toodelete um blob, passar o nome do contêiner de saudação e nome do blob muito**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="6bd51-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="6bd51-161">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="6bd51-161">Delete a blob container</span></span>
<span data-ttu-id="6bd51-162">Finalmente, toodelete um contêiner de blob, passe o nome de contêiner do Olá muito**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="6bd51-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6bd51-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bd51-163">Next steps</span></span>
<span data-ttu-id="6bd51-164">Agora que você aprendeu as Noções básicas sobre Olá Olá serviço blob do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6bd51-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="6bd51-165">Visite Olá [blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="6bd51-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="6bd51-166">Consulte Olá [exemplo de blob de bloco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="6bd51-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="6bd51-167">Consulte Olá [exemplo de blob de página PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="6bd51-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="6bd51-168">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="6bd51-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="6bd51-169">Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="6bd51-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
