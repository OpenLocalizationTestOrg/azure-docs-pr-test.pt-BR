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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="7e82a-104">Como toouse armazenamento de fila do PHP</span><span class="sxs-lookup"><span data-stu-id="7e82a-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="7e82a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7e82a-105">Overview</span></span>
<span data-ttu-id="7e82a-106">Este guia mostrará como cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e82a-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="7e82a-107">exemplos de saudação são gravados por meio de classes do hello SDK do Windows para PHP.</span><span class="sxs-lookup"><span data-stu-id="7e82a-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="7e82a-108">Olá cobertos cenários incluem inserir, inspecionar, obtendo e excluir mensagens da fila, bem como criar e excluir filas.</span><span class="sxs-lookup"><span data-stu-id="7e82a-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="7e82a-109">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="7e82a-109">Create a PHP application</span></span>
<span data-ttu-id="7e82a-110">Olá somente o requisito para criar um aplicativo PHP que acessa o armazenamento de fila do Azure é hello referência de classes de saudação do SDK do Azure para PHP de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="7e82a-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="7e82a-111">Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="7e82a-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="7e82a-112">Neste guia, você usará os recursos do armazenamento de Filas que podem ser chamados dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.</span><span class="sxs-lookup"><span data-stu-id="7e82a-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="7e82a-113">Obter bibliotecas de saudação do cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="7e82a-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="7e82a-114">Configurar seu aplicativo tooaccess armazenamento de fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="7e82a-115">Olá toouse APIs para o armazenamento de fila do Azure, você precisa:</span><span class="sxs-lookup"><span data-stu-id="7e82a-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="7e82a-116">Arquivo de carregador automático de saudação de referência usando Olá [require_once] instrução.</span><span class="sxs-lookup"><span data-stu-id="7e82a-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="7e82a-117">Fazer referência a qualquer classe que possa usar.</span><span class="sxs-lookup"><span data-stu-id="7e82a-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="7e82a-118">Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="7e82a-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="7e82a-119">Este exemplo (e outros exemplos neste artigo) pressupõe que você tenha instalado Olá PHP bibliotecas de cliente para o Azure por meio do criador.</span><span class="sxs-lookup"><span data-stu-id="7e82a-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="7e82a-120">Se você instalou bibliotecas Olá manualmente, você precisará Olá tooreference `WindowsAzure.php` arquivo do carregador automático.</span><span class="sxs-lookup"><span data-stu-id="7e82a-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="7e82a-121">Nos exemplos de saudação abaixo, Olá `require_once` instrução serão sempre mostrada, mas apenas as classes de saudação que são necessárias para tooexecute do exemplo hello serão referenciadas.</span><span class="sxs-lookup"><span data-stu-id="7e82a-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="7e82a-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7e82a-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="7e82a-123">tooinstantiate um cliente de armazenamento de fila do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido.</span><span class="sxs-lookup"><span data-stu-id="7e82a-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="7e82a-124">formato de saudação para cadeia de conexão de serviço de fila de saudação é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="7e82a-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="7e82a-125">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="7e82a-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="7e82a-126">Para acessar o armazenamento de emulador hello:</span><span class="sxs-lookup"><span data-stu-id="7e82a-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="7e82a-127">toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="7e82a-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="7e82a-128">Você pode usar qualquer um dos Olá técnicas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e82a-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="7e82a-129">Passar conexão Olá tooit cadeia de caracteres diretamente.</span><span class="sxs-lookup"><span data-stu-id="7e82a-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="7e82a-130">Use **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="7e82a-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="7e82a-131">Por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="7e82a-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="7e82a-132">Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="7e82a-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="7e82a-133">Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="7e82a-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="7e82a-134">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-134">Create a queue</span></span>
<span data-ttu-id="7e82a-135">Um **QueueRestProxy** objeto permite que você crie uma fila usando Olá **createQueue** método.</span><span class="sxs-lookup"><span data-stu-id="7e82a-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="7e82a-136">Ao criar uma fila, você pode definir opções na fila hello, mas fazer isso não é necessário.</span><span class="sxs-lookup"><span data-stu-id="7e82a-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="7e82a-137">(Olá o exemplo a seguir mostra como tooset metadados em uma fila.)</span><span class="sxs-lookup"><span data-stu-id="7e82a-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="7e82a-138">Você não deve depender de maiúsculas e minúsculas para as chaves de metadados.</span><span class="sxs-lookup"><span data-stu-id="7e82a-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="7e82a-139">Todas as chaves são lidas do serviço de saudação em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7e82a-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="7e82a-140">Adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="7e82a-140">Add a message tooa queue</span></span>
<span data-ttu-id="7e82a-141">tooadd uma fila de tooa de mensagens, use **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="7e82a-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="7e82a-142">método Hello usa o nome da fila hello, texto de mensagem de saudação e opções de mensagem (que são opcionais).</span><span class="sxs-lookup"><span data-stu-id="7e82a-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="7e82a-143">Espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="7e82a-143">Peek at hello next message</span></span>
<span data-ttu-id="7e82a-144">Você pode inspecionar uma (ou mensagens) no início de saudação de uma fila sem removê-la da fila de saudação chamando **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="7e82a-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="7e82a-145">Por padrão, Olá **peekMessage** método retorna uma única mensagem, mas você pode alterar esse valor usando Olá **PeekMessagesOptions -> setNumberOfMessages** método.</span><span class="sxs-lookup"><span data-stu-id="7e82a-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="7e82a-146">Eliminação da fila de mensagem de saudação do próxima</span><span class="sxs-lookup"><span data-stu-id="7e82a-146">De-queue hello next message</span></span>
<span data-ttu-id="7e82a-147">Seu código remove uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="7e82a-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="7e82a-148">Primeiro, você chama **QueueRestProxy -> listMessages**, que torna Olá mensagem invisível tooany outro código que está lendo da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e82a-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="7e82a-149">Por padrão, essa mensagem permanecerá invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="7e82a-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="7e82a-150">(Se a mensagem de saudação não será excluída nesse período de tempo, ela ficará visível na fila de saudação novamente.) toofinish mensagem de saudação remover da fila hello, você deve chamar **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="7e82a-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="7e82a-151">Esse processo de duas etapas de remoção de uma mensagem garante que, quando seu tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou software, outra instância do seu código Olá mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="7e82a-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="7e82a-152">Seu código chama **deleteMessage** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="7e82a-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="7e82a-153">Alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="7e82a-154">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação chamando **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="7e82a-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="7e82a-155">Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="7e82a-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="7e82a-156">saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e, em seguida, define tooextend de tempo limite de visibilidade Olá outro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="7e82a-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="7e82a-157">Isso salva o estado de saudação do trabalho associado à mensagem de saudação e oferece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e82a-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="7e82a-158">Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="7e82a-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="7e82a-159">Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="7e82a-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="7e82a-160">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="7e82a-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="7e82a-161">Opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="7e82a-162">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="7e82a-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="7e82a-163">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="7e82a-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="7e82a-164">Em seguida, você pode definir um limite de visibilidade maior ou menor, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="7e82a-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="7e82a-165">Olá, exemplo de código a seguir usa Olá **getMessages** mensagens tooget 16 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="7e82a-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="7e82a-166">Em seguida, ele processa cada mensagem usando um loop **for** .</span><span class="sxs-lookup"><span data-stu-id="7e82a-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="7e82a-167">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="7e82a-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="7e82a-168">Obter o tamanho da fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-168">Get queue length</span></span>
<span data-ttu-id="7e82a-169">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="7e82a-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="7e82a-170">Olá **QueueRestProxy -> getQueueMetadata** método solicita Olá fila serviço tooreturn metadados sobre a fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e82a-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="7e82a-171">Olá chamada **getApproximateMessageCount** método em Olá retornou objeto fornece uma contagem de quantas mensagens estão em uma fila.</span><span class="sxs-lookup"><span data-stu-id="7e82a-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="7e82a-172">Contagem de saudação só é aproximada pois mensagens podem ser adicionadas ou removidas depois que o serviço de fila Olá responde tooyour solicitação.</span><span class="sxs-lookup"><span data-stu-id="7e82a-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="7e82a-173">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="7e82a-173">Delete a queue</span></span>
<span data-ttu-id="7e82a-174">toodelete uma fila e todas as mensagens de saudação, chame Olá **QueueRestProxy -> deleteQueue** método.</span><span class="sxs-lookup"><span data-stu-id="7e82a-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7e82a-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e82a-175">Next steps</span></span>
<span data-ttu-id="7e82a-176">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="7e82a-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="7e82a-177">Visite Olá [blog da equipe de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="7e82a-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="7e82a-178">Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7e82a-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

