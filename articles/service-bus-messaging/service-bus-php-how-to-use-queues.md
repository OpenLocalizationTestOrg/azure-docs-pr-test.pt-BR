---
title: "filas de aaaHow toouse barramento de serviço com o PHP | Microsoft Docs"
description: "Saiba como filas de toouse barramento de serviço no Azure. Exemplos de código escritos em PHP."
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="e1b4a-104">Como toouse Service Bus filas com PHP</span><span class="sxs-lookup"><span data-stu-id="e1b4a-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="e1b4a-105">Este guia mostra como toouse filas de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="e1b4a-106">exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="e1b4a-107">Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e1b4a-108">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="e1b4a-108">Create a PHP application</span></span>
<span data-ttu-id="e1b4a-109">Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de Blob do Azure Olá Olá referência de classes Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="e1b4a-110">Você pode usar qualquer toocreate de ferramentas de desenvolvimento de seu aplicativo, ou o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="e1b4a-111">A instalação do PHP também deverá ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="e1b4a-112">Neste guia, você usará os recursos de serviço que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="e1b4a-113">Obter Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="e1b4a-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="e1b4a-114">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e1b4a-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="e1b4a-115">fila do barramento de serviço do toouse Olá APIs, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1b4a-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="e1b4a-116">Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require_once] instrução.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="e1b4a-117">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-117">Reference any classes you might use.</span></span>

<span data-ttu-id="e1b4a-118">Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="e1b4a-119">Este exemplo (e outros exemplos neste artigo) supõe que você instalou Olá PHP bibliotecas de cliente para o Azure por meio do criador.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e1b4a-120">Se você instalou bibliotecas Olá manualmente ou como um pacote de PERA, você deve fazer referência a saudação **WindowsAzure.php** arquivo do carregador automático.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="e1b4a-121">Nos exemplos de saudação abaixo, Olá `require_once` instrução sempre será mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="e1b4a-122">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e1b4a-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="e1b4a-123">tooinstantiate um cliente do barramento de serviço, primeiro você deve ter uma cadeia de caracteres de conexão válida neste formato:</span><span class="sxs-lookup"><span data-stu-id="e1b4a-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="e1b4a-124">Onde `Endpoint` normalmente é do formato de saudação `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="e1b4a-125">toocreate qualquer cliente de serviço do Azure, você deve usar o hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="e1b4a-126">Você pode:</span><span class="sxs-lookup"><span data-stu-id="e1b4a-126">You can:</span></span>

* <span data-ttu-id="e1b4a-127">Passar conexão Olá tooit cadeia de caracteres diretamente.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="e1b4a-128">Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="e1b4a-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="e1b4a-129">Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="e1b4a-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="e1b4a-130">Você pode adicionar novas fontes estendendo Olá `ConnectionStringSource` classe</span><span class="sxs-lookup"><span data-stu-id="e1b4a-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="e1b4a-131">Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão de saudação é passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="e1b4a-132">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="e1b4a-132">Create a queue</span></span>
<span data-ttu-id="e1b4a-133">Você pode executar operações de gerenciamento para as filas do barramento de serviço por meio de saudação `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="e1b4a-134">Um `ServiceBusRestProxy` objeto for construído por meio de saudação `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de caracteres de conexão apropriado que encapsula Olá permissões token toomanage-lo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="e1b4a-135">Olá mostrado no exemplo a seguir como tooinstantiate uma `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createQueue` toocreate uma fila denominada `myqueue` dentro de um `MySBNamespace` namespace de serviço:</span><span class="sxs-lookup"><span data-stu-id="e1b4a-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="e1b4a-136">Você pode usar o hello `listQueues` método `ServiceBusRestProxy` objetos toocheck se já existe uma fila com um nome especificado em um namespace.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="e1b4a-137">Mensagens tooa fila de envio</span><span class="sxs-lookup"><span data-stu-id="e1b4a-137">Send messages tooa queue</span></span>
<span data-ttu-id="e1b4a-138">toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `ServiceBusRestProxy->sendQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="e1b4a-139">Olá mostrado no código a seguir como toosend toohello uma mensagem `myqueue` fila criada anteriormente dentro de `MySBNamespace` namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="e1b4a-140">Mensagens de filas de barramento de serviço muito enviadas (e recebidas de) são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="e1b4a-141">[BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos padrão e propriedades que são propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="e1b4a-142">Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e1b4a-143">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e1b4a-144">Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="e1b4a-145">Este limite superior do tamanho da fila é 5 GB.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="e1b4a-146">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="e1b4a-146">Receive messages from a queue</span></span>

<span data-ttu-id="e1b4a-147">Olá melhor maneira tooreceive as mensagens de uma fila é toouse um `ServiceBusRestProxy->receiveQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="e1b4a-148">As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="e1b4a-149">**PeekLock** é saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="e1b4a-150">Ao usar [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , modo de recebimento é uma operação única etapa; ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma fila, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="e1b4a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="e1b4a-152">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="e1b4a-153">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="e1b4a-154">No padrão de saudação [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, recebendo uma mensagem se torna uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e1b4a-155">Ao barramento de serviço recebe uma solicitação, localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores do recebimento e, em seguida, ele retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="e1b4a-156">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber o processo, passando a mensagem de saudação recebida muito`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="e1b4a-157">Quando o Service Bus vê Olá `deleteMessage` chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="e1b4a-158">Olá mostrado no exemplo a seguir como tooreceive e processar uma mensagem usando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (modo de padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e1b4a-159">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="e1b4a-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="e1b4a-160">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e1b4a-161">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método na mensagem recebida (em vez da saudação `deleteMessage` método).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="e1b4a-162">Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e1b4a-163">Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="e1b4a-164">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="e1b4a-165">Isso é geralmente chamado *pelo menos uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="e1b4a-166">Se o cenário de saudação não puder tolerar o processamento duplicado, em seguida, é recomendável adicionar a entrega de mensagens duplicadas lógica adicional tooapplications toohandle.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="e1b4a-167">Isso geralmente é obtido usando Olá `getMessageId` método de mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1b4a-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1b4a-168">Next steps</span></span>
<span data-ttu-id="e1b4a-169">Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e1b4a-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="e1b4a-170">Para obter mais informações, visite também Olá [Centro de desenvolvedores PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e1b4a-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


