---
title: aaaHow toouse armazenamento de fila do PHP | Microsoft Docs
description: "Saiba como toocreate de serviço de armazenamento do toouse Olá fila do Azure e filas de delete e insert, obtenham e excluir mensagens. As amostras são escritas em PHP."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Como toouse armazenamento de fila do PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este guia mostrará como cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Azure. exemplos de saudação são gravados por meio de classes do hello SDK do Windows para PHP. Olá cobertos cenários incluem inserir, inspecionar, obtendo e excluir mensagens da fila, bem como criar e excluir filas.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar um aplicativo PHP
Olá somente o requisito para criar um aplicativo PHP que acessa o armazenamento de fila do Azure é hello referência de classes de saudação do SDK do Azure para PHP de dentro de seu código. Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.

Neste guia, você usará os recursos do armazenamento de Filas que podem ser chamados dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.

## <a name="get-hello-azure-client-libraries"></a>Obter bibliotecas de saudação do cliente do Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar seu aplicativo tooaccess armazenamento de fila
Olá toouse APIs para o armazenamento de fila do Azure, você precisa:

1. Arquivo de carregador automático de saudação de referência usando Olá [require_once] instrução.
2. Fazer referência a qualquer classe que possa usar.

Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.

> [!NOTE]
> Este exemplo (e outros exemplos neste artigo) pressupõe que você tenha instalado Olá PHP bibliotecas de cliente para o Azure por meio do criador. Se você instalou bibliotecas Olá manualmente, você precisará Olá tooreference `WindowsAzure.php` arquivo do carregador automático.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Nos exemplos de saudação abaixo, Olá `require_once` instrução serão sempre mostrada, mas apenas as classes de saudação que são necessárias para tooexecute do exemplo hello serão referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão de armazenamento do Azure
tooinstantiate um cliente de armazenamento de fila do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido. formato de saudação para cadeia de conexão de serviço de fila de saudação é da seguinte maneira.

Para acessar um serviço ao vivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para acessar o armazenamento de emulador hello:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe. Você pode usar qualquer um dos Olá técnicas a seguir:

* Passar conexão Olá tooit cadeia de caracteres diretamente.
* Use **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:
  * Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.
  * Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe.

Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Criar uma fila
Um **QueueRestProxy** objeto permite que você crie uma fila usando Olá **createQueue** método. Ao criar uma fila, você pode definir opções na fila hello, mas fazer isso não é necessário. (Olá o exemplo a seguir mostra como tooset metadados em uma fila.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Você não deve depender de maiúsculas e minúsculas para as chaves de metadados. Todas as chaves são lidas do serviço de saudação em minúsculas.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de mensagens tooa
tooadd uma fila de tooa de mensagens, use **QueueRestProxy -> createMessage**. método Hello usa o nome da fila hello, texto de mensagem de saudação e opções de mensagem (que são opcionais).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Espiar a próxima mensagem de saudação
Você pode inspecionar uma (ou mensagens) no início de saudação de uma fila sem removê-la da fila de saudação chamando **QueueRestProxy -> peekMessages**. Por padrão, Olá **peekMessage** método retorna uma única mensagem, mas você pode alterar esse valor usando Olá **PeekMessagesOptions -> setNumberOfMessages** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>Eliminação da fila de mensagem de saudação do próxima
Seu código remove uma mensagem de uma fila em duas etapas. Primeiro, você chama **QueueRestProxy -> listMessages**, que torna Olá mensagem invisível tooany outro código que está lendo da fila de saudação. Por padrão, essa mensagem permanecerá invisível por 30 segundos. (Se a mensagem de saudação não será excluída nesse período de tempo, ela ficará visível na fila de saudação novamente.) toofinish mensagem de saudação remover da fila hello, você deve chamar **QueueRestProxy -> deleteMessage**. Esse processo de duas etapas de remoção de uma mensagem garante que, quando seu tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou software, outra instância do seu código Olá mesma mensagem e tente novamente. Seu código chama **deleteMessage** logo depois que a mensagem de saudação foi processada.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação chamando **QueueRestProxy -> updateMessage**. Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello. saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e, em seguida, define tooextend de tempo limite de visibilidade Olá outro 60 segundos. Isso salva o estado de saudação do trabalho associado à mensagem de saudação e oferece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação. Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software. Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo. Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Opções adicionais para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila. Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um limite de visibilidade maior ou menor, permitindo que o código mais ou menos tempo toofully processam cada mensagem. Olá, exemplo de código a seguir usa Olá **getMessages** mensagens tooget 16 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **for** . Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Obter o tamanho da fila
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. Olá **QueueRestProxy -> getQueueMetadata** método solicita Olá fila serviço tooreturn metadados sobre a fila de saudação. Olá chamada **getApproximateMessageCount** método em Olá retornou objeto fornece uma contagem de quantas mensagens estão em uma fila. Contagem de saudação só é aproximada pois mensagens podem ser adicionadas ou removidas depois que o serviço de fila Olá responde tooyour solicitação.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Excluir uma fila
toodelete uma fila e todas as mensagens de saudação, chame Olá **QueueRestProxy -> deleteQueue** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento:

* Visite Olá [blog da equipe de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

