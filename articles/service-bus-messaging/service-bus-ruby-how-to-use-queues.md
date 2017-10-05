---
title: "Como usar as filas do Barramento de Serviço do Azure com Ruby | Microsoft Docs"
description: "Aprenda a usar as filas do barramento de serviço no Azure. Exemplos de códigos escritos em Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 357a7277dd42b6973cf35a9f642b8eec36a745e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-ruby"></a><span data-ttu-id="61168-104">Como usar filas do Barramento de Serviço com Ruby</span><span class="sxs-lookup"><span data-stu-id="61168-104">How to use Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="61168-105">Este guia descreve como usar as filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="61168-105">This guide describes how to use Service Bus queues.</span></span> <span data-ttu-id="61168-106">Os exemplos são gravados no Ruby e usam a gema do Azure.</span><span class="sxs-lookup"><span data-stu-id="61168-106">The samples are written in Ruby and use the Azure gem.</span></span> <span data-ttu-id="61168-107">Os cenários cobertos incluem **criar filas, enviar e receber mensagens** e **excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="61168-107">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="61168-108">Para saber mais sobre filas de Barramento de Serviços, confira a seção [Próximas etapas](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="61168-108">For more information about Service Bus queues, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="61168-109">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="61168-109">How to create a queue</span></span>
<span data-ttu-id="61168-110">O objeto**Azure::ServiceBusService** permite que você trabalhe com filas.</span><span class="sxs-lookup"><span data-stu-id="61168-110">The **Azure::ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="61168-111">Para criar uma fila, use o método `create_queue()`.</span><span class="sxs-lookup"><span data-stu-id="61168-111">To create a queue, use the `create_queue()` method.</span></span> <span data-ttu-id="61168-112">O exemplo a seguir cria uma fila ou imprime os erros, se houver algum.</span><span class="sxs-lookup"><span data-stu-id="61168-112">The following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="61168-113">Você também pode passar em um objeto **Azure::ServiceBus::Queue** com opções adicionais, que permite a substituição de configurações padrão da fila, assim como a vida útil da mensagem ou o tamanho máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="61168-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size.</span></span> <span data-ttu-id="61168-114">O exemplo a seguir mostra como definir o tamanho máximo da fila como 5 GB e a vida útil como 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="61168-114">The following example shows how to set the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="61168-115">Como enviar mensagens para uma fila</span><span class="sxs-lookup"><span data-stu-id="61168-115">How to send messages to a queue</span></span>
<span data-ttu-id="61168-116">Para enviar uma mensagem a uma fila do Barramento de Serviço, o aplicativo chama o método `send_queue_message()` no objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="61168-116">To send a message to a Service Bus queue, your application calls the `send_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="61168-117">Mensagens enviadas para (e recebidas de) as filas do Barramento de Serviço são objetos **Azure::ServiceBus::BrokeredMessage** e têm um conjunto de propriedades padrão (como `label` e `time_to_live`), um dicionário que é usado para manter propriedades personalizadas específicas ao aplicativo e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61168-117">Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="61168-118">Um aplicativo pode definir o corpo da mensagem, passando um valor da cadeia de caracteres como a mensagem, e qualquer propriedade padrão necessária será preenchida com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="61168-118">An application can set the body of the message by passing a string value as the message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="61168-119">O exemplo a seguir demonstra como enviar uma mensagem de teste à fila chamada `test-queue` usando `send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="61168-119">The following example demonstrates how to send a test message to the queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="61168-120">As filas do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="61168-120">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="61168-121">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="61168-121">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="61168-122">Não há nenhum limite no número de mensagens mantidas em uma fila mas há uma capacidade do tamanho total das mensagens mantidas por uma fila.</span><span class="sxs-lookup"><span data-stu-id="61168-122">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="61168-123">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="61168-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="61168-124">Como receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="61168-124">How to receive messages from a queue</span></span>
<span data-ttu-id="61168-125">As mensagens são recebidas de uma fila usando o método `receive_queue_message()` no objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="61168-125">Messages are received from a queue using the `receive_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="61168-126">Por padrão, as mensagens são lidas e bloqueadas sem excluí-las da fila.</span><span class="sxs-lookup"><span data-stu-id="61168-126">By default, messages are read and locked without being deleted from the queue.</span></span> <span data-ttu-id="61168-127">Entretanto, você pode excluir mensagens da fila à medida que são lidas ao configurar a opção `:peek_lock` como **false**.</span><span class="sxs-lookup"><span data-stu-id="61168-127">However, you can delete messages from the queue as they are read by setting the `:peek_lock` option to **false**.</span></span>

<span data-ttu-id="61168-128">O comportamento padrão faz com que a leitura e a exclusão se dividam em uma operação de dois estágios, o que também torna possível o suporte a aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="61168-128">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="61168-129">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61168-129">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="61168-130">Depois que o aplicativo termina de processar a mensagem (ou a armazena de forma segura para um processamento futuro), ele conclui o segundo estágio do processo de recebimento, chamando o método `delete_queue_message()` e fornecendo a mensagem a ser excluída como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="61168-130">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_queue_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="61168-131">O método `delete_queue_message()` marcará a mensagem como tendo sido consumida e a removerá da fila.</span><span class="sxs-lookup"><span data-stu-id="61168-131">The `delete_queue_message()` method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="61168-132">Se o parâmetro `:peek_lock` estiver definido como **false**, a leitura e a exclusão da mensagem se tornam o modelo mais simples e funcionam melhor em cenários nos quais o aplicativo pode tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="61168-132">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="61168-133">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="61168-133">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="61168-134">Como o Barramento de Serviço marca a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="61168-134">Because Service Bus has marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="61168-135">O exemplo a seguir demonstra como receber e processar mensagens usando `receive_queue_message()`.</span><span class="sxs-lookup"><span data-stu-id="61168-135">The following example demonstrates how to receive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="61168-136">O exemplo primeiro recebe e exclui uma mensagem usando `:peek_lock` definido como **false**, então recebe outra mensagem e exclui a mensagem usando `delete_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="61168-136">The example first receives and deletes a message by using `:peek_lock` set to **false**, then it receives another message and then deletes the message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="61168-137">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="61168-137">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="61168-138">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="61168-138">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="61168-139">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele chamará o método `unlock_queue_message()` no objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="61168-139">If a receiver application is unable to process the message for some reason, then it can call the `unlock_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="61168-140">Essa chamada fará com que o Barramento de Serviço desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="61168-140">This call causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="61168-141">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se houver falha no processamento da mensagem pelo aplicativo da expiração do tempo limite de bloqueio (por exemplo, se o aplicativo travar), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="61168-141">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="61168-142">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método `delete_queue_message()` seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="61168-142">In the event that the application crashes after processing the message but before the `delete_queue_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="61168-143">Esse processo é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez, mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="61168-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="61168-144">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="61168-144">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="61168-145">Isso geralmente é realizado usando a propriedade `message_id` da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="61168-145">This is often achieved using the `message_id` property of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61168-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61168-146">Next steps</span></span>
<span data-ttu-id="61168-147">Agora que você já sabe as noções básicas das filas de Barramento de Serviço, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="61168-147">Now that you've learned the basics of Service Bus queues, follow these links to learn more.</span></span>

* <span data-ttu-id="61168-148">Visão geral de [filas, tópicos e assinaturas](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="61168-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="61168-149">Visite o repositório [SDK do Azure para o Ruby](https://github.com/Azure/azure-sdk-for-ruby) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="61168-149">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="61168-150">Para fazer uma comparação entre as filas de Barramento de Serviço do Azure discutidas nesse artigo e as filas do Azure discutidas no artigo [Como usar o armazenamento de Filas no Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md), confira [Filas do Azure e filas de Barramento de Serviço do Azure - Comparadas e Contrastadas](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="61168-150">For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

