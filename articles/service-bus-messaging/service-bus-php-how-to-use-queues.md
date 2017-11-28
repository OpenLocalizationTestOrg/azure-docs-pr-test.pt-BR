---
title: "Como usar as filas de Barramento de Serviço com PHP | Microsoft Docs"
description: "Aprenda a usar as filas do barramento de serviço no Azure. Exemplos de código escritos em PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="6f3c9-104">Como usar filas do Barramento de Serviço com PHP</span><span class="sxs-lookup"><span data-stu-id="6f3c9-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="6f3c9-105">Este guia mostra como usar as filas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="6f3c9-106">As amostras são escritas em PHP e usam o [SDK do Azure para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="6f3c9-107">Os cenários cobertos incluem **criar filas**, **enviar e receber mensagens** e **excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="6f3c9-108">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="6f3c9-108">Create a PHP application</span></span>
<span data-ttu-id="6f3c9-109">O único requisito para a criação de um aplicativo PHP que acessa o serviço Blob do Azure é a referência de classes no [SDK do Azure para PHP](../php-download-sdk.md) em seu código.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="6f3c9-110">Você pode usar quaisquer ferramentas de desenvolvimento para criar seu aplicativo, ou o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="6f3c9-111">A instalação do PHP também deve ter a [extensão OpenSSL](http://php.net/openssl) instalada e habilitada.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="6f3c9-112">Neste guia, você usará os recursos de serviço que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="6f3c9-113">Obter as bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="6f3c9-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="6f3c9-114">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="6f3c9-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="6f3c9-115">Para usar as APIs da fila do Barramento de Serviço, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="6f3c9-116">Faça referência ao arquivo do carregador automático usando a instrução [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="6f3c9-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="6f3c9-117">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-117">Reference any classes you might use.</span></span>

<span data-ttu-id="6f3c9-118">O exemplo a seguir mostra como incluir o arquivo de carregador automático e fazer referência à classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="6f3c9-119">Este exemplo (e outros exemplos neste artigo) pressupõe que você instalou as Bibliotecas de Cliente PHP para Azure por meio do Compositor.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="6f3c9-120">Se você instalou as bibliotecas manualmente ou como um pacote PEAR, será necessário fazer referência ao arquivo de carregador automático **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="6f3c9-121">Nos exemplos abaixo, a instrução `require_once` será mostrada sempre, mas somente as classes necessárias para executar o exemplo serão referenciadas.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="6f3c9-122">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6f3c9-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="6f3c9-123">Para criar uma instância do cliente do Barramento de Serviço, você deve ter primeiro uma cadeia de conexão válida neste formato:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="6f3c9-124">Em que `Endpoint` geralmente está no formato `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="6f3c9-125">Para criar um cliente de serviço do Azure, é necessário usar a classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="6f3c9-126">Você pode:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-126">You can:</span></span>

* <span data-ttu-id="6f3c9-127">Passar a cadeia de conexão diretamente para ele.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="6f3c9-128">Usar **CloudConfigurationManager (CCM)** para verificar várias fontes externas da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="6f3c9-129">Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="6f3c9-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="6f3c9-130">você pode adicionar novas origens ao estender a classe `ConnectionStringSource`</span><span class="sxs-lookup"><span data-stu-id="6f3c9-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="6f3c9-131">Para os exemplos descritos aqui, a cadeia de conexão é passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="6f3c9-132">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="6f3c9-132">Create a queue</span></span>
<span data-ttu-id="6f3c9-133">Você pode executar operações de gerenciamento de filas do Barramento de Serviço por meio da classe `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="6f3c9-134">Um objeto `ServiceBusRestProxy` é construído com o método de fábrica `ServicesBuilder::createServiceBusService` com uma cadeia de conexão apropriada que encapsula as permissões de token para gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="6f3c9-135">O exemplo a seguir mostra como instanciar um `ServiceBusRestProxy` e chamar um `ServiceBusRestProxy->createQueue` para criar uma fila denominada `myqueue` dentro de um namespace de serviço `MySBNamespace`:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="6f3c9-136">Você pode usar o método `listQueues` em objetos `ServiceBusRestProxy` para verificar se já existe uma fila com um nome especificado em um namespace.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="6f3c9-137">Enviar mensagens a uma fila</span><span class="sxs-lookup"><span data-stu-id="6f3c9-137">Send messages to a queue</span></span>
<span data-ttu-id="6f3c9-138">Para enviar uma mensagem para uma fila do Barramento de Serviço, seu aplicativo chamará o método `ServiceBusRestProxy->sendQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="6f3c9-139">O código abaixo demonstra como enviar uma mensagem à fila `myqueue` que criamos acima no namespace de serviço `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="6f3c9-140">As mensagens enviadas para (e recebidas de) filas de Barramento de Serviço são instâncias da classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="6f3c9-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="6f3c9-141">Os objetos [BrokeredMessage][BrokeredMessage] têm um conjunto de propriedades e métodos padrão que são usados para manter as propriedades personalizadas específicas do aplicativo e um corpo de dados de aplicativo arbitrários.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="6f3c9-142">As filas do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="6f3c9-143">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="6f3c9-144">Não há nenhum limite no número de mensagens mantidas em uma fila mas há uma capacidade do tamanho total das mensagens mantidas por uma fila.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="6f3c9-145">Este limite superior do tamanho da fila é 5 GB.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="6f3c9-146">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="6f3c9-146">Receive messages from a queue</span></span>

<span data-ttu-id="6f3c9-147">A melhor maneira de receber mensagens de uma fila é usar um método `ServiceBusRestProxy->receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="6f3c9-148">As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="6f3c9-149">**PeekLock** é o padrão.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="6f3c9-150">Ao usar o modo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete), o recebimento é uma operação única, isto é, quando o Barramento de Serviço recebe uma solicitação de leitura de uma mensagem em uma fila, ele marca a mensagem como sendo consumida e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="6f3c9-151">O modo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo pode tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="6f3c9-152">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="6f3c9-153">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="6f3c9-154">No modo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) padrão, o recebimento de uma mensagem se torna uma operação de dois estágios, o que possibilita o suporte a aplicativos que não podem tolerar ausência de mensagens.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="6f3c9-155">Quando o Barramento de Serviço recebe uma solicitação, ele localiza a próxima mensagem a ser consumida, bloqueia-a para evitar que outros consumidores a recebam e, em seguida, retorna-a para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="6f3c9-156">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para processamento futuro), ele conclui a segunda etapa do processo de recebimento encaminhando a mensagem recebida para `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="6f3c9-157">Quando o Barramento de Serviço vê a chamada `deleteMessage`, ele marca a mensagem como tendo sido consumida e a remove da fila.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="6f3c9-158">O exemplo a seguir mostra como receber e processar uma mensagem usando o modo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (o modo padrão).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="6f3c9-159">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="6f3c9-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="6f3c9-160">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="6f3c9-161">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele poderá chamar o método `unlockMessage` na mensagem recebida (em vez do método `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="6f3c9-162">Isso fará com que o Service Bus desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="6f3c9-163">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se o aplicativo não conseguir processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, em caso de falha do aplicativo), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="6f3c9-164">Se houver falha do aplicativo após o processamento da mensagem, mas antes que a solicitação `deleteMessage` seja gerada, a mensagem será entregue novamente ao aplicativo quando ele reiniciar.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="6f3c9-165">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez, mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="6f3c9-166">Se o cenário não puder tolerar o processamento duplicado, é recomendável adicionar lógica extra ao aplicativo para tratar a entrega de mensagens duplicadas.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="6f3c9-167">Isso geralmente é realizado usando o método `getMessageId` da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f3c9-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f3c9-168">Next steps</span></span>
<span data-ttu-id="6f3c9-169">Agora que você aprendeu as noções básicas sobre as filas do Barramento de Serviço, veja [Filas, tópicos e assinaturas][Queues, topics, and subscriptions] para saber mais.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="6f3c9-170">Para saber mais, visite também o [Centro de Desenvolvedores em PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


