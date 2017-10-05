---
title: Como usar o Armazenamento de Filas do PHP | Microsoft Docs
description: "Saiba como usar o serviço de armazenamento de Filas do Azure para criar e excluir filas, bem como para inserir, obter e excluir mensagens. As amostras são escritas em PHP."
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
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="85bf0-104">Como usar o Armazenamento de Fila do PHP</span><span class="sxs-lookup"><span data-stu-id="85bf0-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="85bf0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="85bf0-105">Overview</span></span>
<span data-ttu-id="85bf0-106">Este guia lhe mostrará como executar cenários comuns usando o serviço de Armazenamento de Fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="85bf0-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="85bf0-107">Os exemplos são gravados usando classes do SDK do Windows para PHP.</span><span class="sxs-lookup"><span data-stu-id="85bf0-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="85bf0-108">Os cenários abrangidos incluem inserir, exibir, obter e excluir mensagens da fila, bem como criar e excluir filas.</span><span class="sxs-lookup"><span data-stu-id="85bf0-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="85bf0-109">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="85bf0-109">Create a PHP application</span></span>
<span data-ttu-id="85bf0-110">O único requisito para a criação de um aplicativo PHP que acessa o armazenamento de Filas do Azure é a referência das classes do SDK do Azure para PHP de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="85bf0-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="85bf0-111">Você pode usar as ferramentas de desenvolvimento para criar seu aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="85bf0-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="85bf0-112">Neste guia, você usará os recursos do armazenamento de Filas que podem ser chamados dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.</span><span class="sxs-lookup"><span data-stu-id="85bf0-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="85bf0-113">Obter as bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="85bf0-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="85bf0-114">Configurar seu aplicativo para acessar o armazenamento de Filas</span><span class="sxs-lookup"><span data-stu-id="85bf0-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="85bf0-115">Para usar as APIs de armazenamento de Filas do Azure, você precisa:</span><span class="sxs-lookup"><span data-stu-id="85bf0-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="85bf0-116">Fazer referência ao arquivo do carregador automático usando a instrução [require_once].</span><span class="sxs-lookup"><span data-stu-id="85bf0-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="85bf0-117">Fazer referência a qualquer classe que possa usar.</span><span class="sxs-lookup"><span data-stu-id="85bf0-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="85bf0-118">O exemplo a seguir mostra como incluir o arquivo de carregador automático e fazer referência à classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="85bf0-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="85bf0-119">Este exemplo (e outros exemplos neste artigo) pressupõe que você instalou as Bibliotecas de Cliente PHP para Azure por meio do Compositor.</span><span class="sxs-lookup"><span data-stu-id="85bf0-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="85bf0-120">Se tiver instalado as bibliotecas manualmente, você precisará fazer referência ao arquivo de carregador automático `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="85bf0-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="85bf0-121">Nos exemplos abaixo, a instrução `require_once` será mostrada sempre, mas somente as classes que são necessárias para executar o exemplo serão referenciadas.</span><span class="sxs-lookup"><span data-stu-id="85bf0-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="85bf0-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="85bf0-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="85bf0-123">Para criar uma instância de um cliente de armazenamento de Filas do Azure, você deve primeiramente ter uma cadeia de conexão válida.</span><span class="sxs-lookup"><span data-stu-id="85bf0-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="85bf0-124">O formato da cadeia de conexão do serviço Fila é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="85bf0-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="85bf0-125">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="85bf0-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="85bf0-126">Para acessar o armazenamento do emulador:</span><span class="sxs-lookup"><span data-stu-id="85bf0-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="85bf0-127">Para criar qualquer cliente de serviço do Azure, é necessário usar a classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="85bf0-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="85bf0-128">É possível usar qualquer uma das técnicas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85bf0-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="85bf0-129">Passar a cadeia de conexão diretamente para ele.</span><span class="sxs-lookup"><span data-stu-id="85bf0-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="85bf0-130">Use **CloudConfigurationManager (CCM)** para verificar várias fontes externas da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="85bf0-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="85bf0-131">Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="85bf0-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="85bf0-132">É possível adicionar novas origens ao estender a classe **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="85bf0-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="85bf0-133">Para os exemplos descritos aqui, a cadeia de conexão será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="85bf0-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="85bf0-134">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-134">Create a queue</span></span>
<span data-ttu-id="85bf0-135">O objeto **QueueRestProxy** permite que você crie uma fila com o método **createQueue**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="85bf0-136">Ao criar uma fila, você pode definir opções na fila, mas fazer isso não é necessário.</span><span class="sxs-lookup"><span data-stu-id="85bf0-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="85bf0-137">(O exemplo abaixo mostra como definir metadados em uma fila.)</span><span class="sxs-lookup"><span data-stu-id="85bf0-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="85bf0-138">Você não deve depender de maiúsculas e minúsculas para as chaves de metadados.</span><span class="sxs-lookup"><span data-stu-id="85bf0-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="85bf0-139">Todas as chaves são lidas do serviço em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="85bf0-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="85bf0-140">Adicionar uma mensagem a uma fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-140">Add a message to a queue</span></span>
<span data-ttu-id="85bf0-141">Para adicionar uma mensagem para uma fila, use **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="85bf0-142">O método utiliza o nome da fila, o texto da mensagem e opções de mensagem (que são opcionais).</span><span class="sxs-lookup"><span data-stu-id="85bf0-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="85bf0-143">Espiar a próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="85bf0-143">Peek at the next message</span></span>
<span data-ttu-id="85bf0-144">Você pode exibir uma mensagem (ou mensagens) na frente de uma fila sem removê-la da fila chamando **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="85bf0-145">Por padrão, o método **peekMessage** retorna uma única mensagem, mas você pode alterar esse valor usando o método **PeekMessagesOptions->setNumberOfMessages**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="85bf0-146">Remover a próxima mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-146">De-queue the next message</span></span>
<span data-ttu-id="85bf0-147">Seu código remove uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="85bf0-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="85bf0-148">Primeiro, você chama **QueueRestProxy->listMessages**, que torna a mensagem invisível para qualquer outro código de leitura da fila.</span><span class="sxs-lookup"><span data-stu-id="85bf0-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="85bf0-149">Por padrão, essa mensagem permanecerá invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="85bf0-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="85bf0-150">(Se a mensagem não for excluída neste período de tempo, ela se tornará visível na fila novamente.) Para terminar de remover a mensagem da fila, você deve chamar **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="85bf0-151">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="85bf0-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="85bf0-152">Seu código chama **deleteMessage** logo depois que a mensagem é processada.</span><span class="sxs-lookup"><span data-stu-id="85bf0-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="85bf0-153">Alterar o conteúdo de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-153">Change the contents of a queued message</span></span>
<span data-ttu-id="85bf0-154">Você pode alterar o conteúdo de uma mensagem in-loco na fila chamando **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="85bf0-155">Se a mensagem representar uma tarefa de trabalho, você poderá usar esse recurso para atualizar o status da tarefa de trabalho.</span><span class="sxs-lookup"><span data-stu-id="85bf0-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="85bf0-156">O código a seguir atualiza a mensagem da fila com novo conteúdo e define o tempo limite de visibilidade para estender mais 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="85bf0-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="85bf0-157">Isso salva o estado do trabalho que está associado à mensagem e dá ao cliente mais um minuto para continuar trabalhando na mensagem.</span><span class="sxs-lookup"><span data-stu-id="85bf0-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="85bf0-158">Você pode usar essa técnica para acompanhar fluxos de trabalho de várias etapas em mensagens em fila, sem a necessidade de começar desde o início, caso uma etapa de processamento falhar devido a uma falha de hardware ou de software.</span><span class="sxs-lookup"><span data-stu-id="85bf0-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="85bf0-159">Normalmente, você mantém uma contagem de repetições e, se a mensagem for repetida mais de *n* vezes, você a exclui.</span><span class="sxs-lookup"><span data-stu-id="85bf0-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="85bf0-160">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="85bf0-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="85bf0-161">Opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="85bf0-162">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="85bf0-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="85bf0-163">Primeiro, você pode obter um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="85bf0-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="85bf0-164">Segundo, você pode definir um tempo limite de visibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="85bf0-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="85bf0-165">O seguinte exemplo de código usa o método **getMessages** para receber 16 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="85bf0-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="85bf0-166">Em seguida, ele processa cada mensagem usando um loop **for** .</span><span class="sxs-lookup"><span data-stu-id="85bf0-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="85bf0-167">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="85bf0-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="85bf0-168">Obter o tamanho da fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-168">Get queue length</span></span>
<span data-ttu-id="85bf0-169">Você pode obter uma estimativa do número de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="85bf0-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="85bf0-170">O método **QueueRestProxy->getQueueMetadata** solicita que o serviço Fila retorne os metadados sobre a fila.</span><span class="sxs-lookup"><span data-stu-id="85bf0-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="85bf0-171">Chamando o método **getApproximateMessageCount** no objeto retornado fornece uma contagem de quantas mensagens estão em uma fila.</span><span class="sxs-lookup"><span data-stu-id="85bf0-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="85bf0-172">A contagem é aproximada apenas porque as mensagens podem ser adicionadas ou removidas depois que o serviço Fila responde à sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="85bf0-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="85bf0-173">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="85bf0-173">Delete a queue</span></span>
<span data-ttu-id="85bf0-174">Para excluir uma fila e todas as mensagens nela, chame o método **QueueRestProxy->deleteQueue**.</span><span class="sxs-lookup"><span data-stu-id="85bf0-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="85bf0-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85bf0-175">Next steps</span></span>
<span data-ttu-id="85bf0-176">Agora que você aprendeu os conceitos básicos do armazenamento de Filas do Azure, siga estes links para saber mais sobre tarefas de armazenamento mais complexas:</span><span class="sxs-lookup"><span data-stu-id="85bf0-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="85bf0-177">Visite o [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="85bf0-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="85bf0-178">Para saber mais, veja também a [Central de desenvolvedores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="85bf0-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
<span data-ttu-id="85bf0-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span><span class="sxs-lookup"><span data-stu-id="85bf0-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span></span>
[Azure Portal]: https://portal.azure.com

