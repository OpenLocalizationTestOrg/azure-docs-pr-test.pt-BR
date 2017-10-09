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
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Como toouse blob storage do PHP
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este guia mostra como os cenários comuns de tooperform usando hello Azure serviço de blob. exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP][download]. Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs. Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar um aplicativo PHP
Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de blob do Azure Olá Olá referência de classes hello Azure SDK para PHP de dentro de seu código. Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.

Neste guia, você usará os recursos de serviços que podem ser chamados em um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, uma função de trabalho ou um site.

## <a name="get-hello-azure-client-libraries"></a>Obter bibliotecas de saudação do cliente do Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Configurar o serviço de blob do aplicativo tooaccess Olá
toouse hello Azure APIs do serviço blob, você precisa:

1. Arquivo de carregador automático de saudação de referência usando Olá [require_once] instrução, e
2. Fazer referência a qualquer classe que você possa usar.

Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.

> [!NOTE]
> exemplos de Olá neste artigo presumem que você instalou Olá bibliotecas de cliente do PHP para o Azure por meio do criador. Se você instalou bibliotecas Olá manualmente, você precisa Olá tooreference `WindowsAzure.php` arquivo do carregador automático.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de saudação abaixo, Olá `require_once` instrução serão sempre mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão de armazenamento do Azure
tooinstantiate um cliente do serviço blob do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido. cadeia de conexão de serviço de blob Olá Olá formato é:

Para acessar um serviço ao vivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para acessar o emulador de armazenamento hello:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe. Você pode:

* passar conexão Olá tooit cadeia de caracteres diretamente ou
* Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:
  * Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.
  * Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe.

Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Criar um contêiner
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Um **BlobRestProxy** objeto permite que você crie um contêiner de blob com hello **createContainer** método. Ao criar um contêiner, você pode definir opções no contêiner hello, mas fazer isso não é necessário. (o exemplo hello abaixo mostra como contêiner de saudação tooset acesso (ACL) da lista de controle e os metadados do contêiner.)

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

Chamando **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOBS)** torna Olá contêiner e blob de dados acessíveis via solicitações anônimas. A chamada a **setPublicAccess(PublicAccessType::BLOBS_ONLY)** tornam apenas os dados do blob acessíveis por meio de solicitações anônimas. Para obter mais informações sobre as ACLs do contêiner, consulte [Set Container ACL (REST API)][container-acl] (Definir a ACL do contêiner [API REST]).

Para obter mais informações sobre os códigos de erro do serviço Blob, consulte [Blob Service Error Codes][error-codes] (Códigos de erro do serviço Blob).

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
tooupload um arquivo como um blob, use Olá **BlobRestProxy -> createBlockBlob** método. Essa operação cria blob Olá se ele não existe ou substitui-lo se ele faz. Hello exemplo de código a seguir supõe que esse contêiner Olá já foi criado e usa [fopen] [ fopen] tooopen arquivo de saudação como um fluxo.

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

Observe que o exemplo anterior de Olá carrega um blob como um fluxo. No entanto, um blob também pode ser carregado como uma cadeia de caracteres usando, por exemplo, Olá [arquivo\_obter\_conteúdo] [ file_get_contents] função. toodo este usando o exemplo anterior hello, altere `$content = fopen("c:\myfile.txt", "r");` muito`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, use Olá **BlobRestProxy -> listBlobs** método com um **foreach** tooloop por meio do resultado de saudação de loop. Olá código a seguir exibe o nome de saudação de cada blob como a saída em um contêiner e exibe seu navegador de toohello do URI.

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

## <a name="download-a-blob"></a>Baixar um blob
toodownload um blob, chamada hello **BlobRestProxy -> getBlob** método, então a saudação da chamada **getContentStream** método hello resultante **GetBlobResult** objeto.

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

Observe que esse exemplo hello acima obtém um blob como um recurso de fluxo (comportamento padrão de saudação). No entanto, você pode usar o hello [fluxo\_obter\_conteúdo] [ stream-get-contents] saudação do função tooconvert retornou uma cadeia tooa fluxo.

## <a name="delete-a-blob"></a>Excluir um blob
toodelete um blob, passar o nome do contêiner de saudação e nome do blob muito**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Excluir um contêiner de blob
Finalmente, toodelete um contêiner de blob, passe o nome de contêiner do Olá muito**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço blob do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* Visite Olá [blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Consulte Olá [exemplo de blob de bloco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Consulte Olá [exemplo de blob de página PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Transferência de dados com hello AzCopy utilitário de linha de comando](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
