---
title: "Como usar as filas do Barramento de Serviço do Azure com Java | Microsoft Docs"
description: "Aprenda a usar as filas do barramento de serviço no Azure. Exemplos de códigos escritos em Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 170f431525ffdc93a01fc085e48e69c3a774968e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-java"></a><span data-ttu-id="ea41d-104">Como usar filas do Barramento de Serviço com Java</span><span class="sxs-lookup"><span data-stu-id="ea41d-104">How to use Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="ea41d-105">Este artigo descreve como usar as filas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="ea41d-105">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="ea41d-106">As amostras são gravadas em Java e usam o [SDK do Azure para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="ea41d-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="ea41d-107">Os cenários cobertos incluem **criar filas**, **enviar e receber mensagens** e **excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="ea41d-108">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ea41d-108">Configure your application to use Service Bus</span></span>
<span data-ttu-id="ea41d-109">Verifique se você instalou o [SDK do Azure para Java][Azure SDK for Java] antes de compilar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="ea41d-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="ea41d-110">Se estiver usando o Eclipse, instale o [Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse], que inclui o SDK do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="ea41d-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="ea41d-111">Você pode adicionar as **Bibliotecas do Microsoft Azure para Java** ao seu projeto:</span><span class="sxs-lookup"><span data-stu-id="ea41d-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="ea41d-112">Adicione as seguintes instruções `import` à parte superior do arquivo Java:</span><span class="sxs-lookup"><span data-stu-id="ea41d-112">Add the following `import` statements to the top of the Java file:</span></span>

```java
// Include the following imports to use Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="ea41d-113">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="ea41d-113">Create a queue</span></span>
<span data-ttu-id="ea41d-114">Operações de gerenciamento para as filas do Barramento de Serviço podem ser realizadas pela classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="ea41d-115">Um objeto **ServiceBusContract** é construído com uma configuração adequada que encapsula o token SAS com as permissões para gerenciá-lo, e a classe **ServiceBusContract** é o único ponto de comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ea41d-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="ea41d-116">A classe **ServiceBusService** fornece métodos para criar, enumerar e excluir filas.</span><span class="sxs-lookup"><span data-stu-id="ea41d-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span></span> <span data-ttu-id="ea41d-117">O exemplo abaixo mostra como um objeto **ServiceBusService** pode ser usado para criar uma fila chamada `TestQueue` com um namespace chamado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="ea41d-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="ea41d-118">Existem métodos em `QueueInfo` que permitem que as propriedades da fila sejam ajustadas (por exemplo, para definir o valor da "vida útil" (TTL) padrão a ser aplicado às mensagens enviadas para a fila).</span><span class="sxs-lookup"><span data-stu-id="ea41d-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span></span> <span data-ttu-id="ea41d-119">O exemplo a seguir mostra como criar uma fila denominada `TestQueue` com um tamanho máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="ea41d-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="ea41d-120">Observe que você pode usar o método `listQueues` em objetos **ServiceBusContract** para verificar se já existe uma fila com um nome especificado dentro de um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="ea41d-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="ea41d-121">Enviar mensagens a uma fila</span><span class="sxs-lookup"><span data-stu-id="ea41d-121">Send messages to a queue</span></span>
<span data-ttu-id="ea41d-122">Para enviar uma mensagem a uma fila do Barramento de Serviço, seu aplicativo obterá um objeto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="ea41d-123">O código abaixo demonstra como enviar uma mensagem à fila `TestQueue` que criamos acima no namespace `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="ea41d-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="ea41d-124">As mensagens enviadas para (e recebidas de) filas de Barramento de Serviço são instâncias da classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="ea41d-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="ea41d-125">Os objetos [BrokeredMessage][BrokeredMessage] têm um conjunto de propriedades padrão (como [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário usado para manter as propriedades personalizadas específicas do aplicativo e um corpo de dados de aplicativo arbitrários.</span><span class="sxs-lookup"><span data-stu-id="ea41d-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="ea41d-126">Um aplicativo pode definir o corpo da mensagem passando qualquer objeto serializável para o construtor do [BrokeredMessage][BrokeredMessage] e o serializador adequado será, então, usado para serializar o objeto.</span><span class="sxs-lookup"><span data-stu-id="ea41d-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span></span> <span data-ttu-id="ea41d-127">Como alternativa, você pode fornecer um objeto **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="ea41d-128">O exemplo a seguir demonstra como enviar cinco mensagens de teste para o objeto `TestQueue`**MessageSender** obtido no trecho de código anterior:</span><span class="sxs-lookup"><span data-stu-id="ea41d-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for the body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message to the queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="ea41d-129">As filas do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ea41d-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ea41d-130">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ea41d-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ea41d-131">Não há nenhum limite no número de mensagens mantidas em uma fila mas há uma capacidade do tamanho total das mensagens mantidas por uma fila.</span><span class="sxs-lookup"><span data-stu-id="ea41d-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="ea41d-132">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ea41d-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="ea41d-133">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="ea41d-133">Receive messages from a queue</span></span>
<span data-ttu-id="ea41d-134">A maneira mais fácil de receber mensagens de uma fila é usar um objeto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="ea41d-135">As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="ea41d-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="ea41d-136">Ao usar o modo **ReceiveAndDelete**, o recebimento é uma operação única, isto é, quando o Barramento de Serviço recebe uma solicitação de leitura de uma mensagem em uma fila, ele marca a mensagem como sendo consumida e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea41d-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="ea41d-137">O modo **ReceiveAndDelete** (que é o modo padrão) é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo possa tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="ea41d-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="ea41d-138">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="ea41d-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span>
<span data-ttu-id="ea41d-139">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="ea41d-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="ea41d-140">No modo **PeekLock**, o recebimento de uma mensagem se torna uma operação de dois estágios, o que possibilita o suporte aos aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="ea41d-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ea41d-141">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea41d-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="ea41d-142">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para processamento futuro), ele conclui a segunda etapa do processo de recebimento chamando **Delete** na mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="ea41d-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="ea41d-143">Quando o Barramento de Serviço vê a chamada **Delete**, ele marca a mensagem como tendo sido consumida e a remove da fila.</span><span class="sxs-lookup"><span data-stu-id="ea41d-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="ea41d-144">O exemplo a seguir demonstra como as mensagens podem ser recebidas e processadas usando o modo **PeekLock** (não o modo padrão).</span><span class="sxs-lookup"><span data-stu-id="ea41d-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="ea41d-145">O exemplo abaixo executa um loop infinito e processa mensagens assim que elas chegam em nossa `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="ea41d-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ea41d-146">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="ea41d-146">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ea41d-147">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="ea41d-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ea41d-148">Se um aplicativo receptor não for capaz de processar a mensagem por algum motivo, ele chamará o método **unlockMessage** na mensagem recebida (em vez do método **deleteMessage**).</span><span class="sxs-lookup"><span data-stu-id="ea41d-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="ea41d-149">Isso fará com que o Barramento de Serviço desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="ea41d-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ea41d-150">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se houver falha no processamento da mensagem pelo aplicativo da expiração do tempo limite de bloqueio (por exemplo, se o aplicativo travar), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="ea41d-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="ea41d-151">Se houver falha do aplicativo após o processamento da mensagem, mas antes da solicitação **deleteMessage** ser emitida, a mensagem será entregue novamente ao aplicativo quando ele reiniciar.</span><span class="sxs-lookup"><span data-stu-id="ea41d-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="ea41d-152">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez, mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="ea41d-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="ea41d-153">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="ea41d-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="ea41d-154">Isso geralmente é feito com o método **getMessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="ea41d-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea41d-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea41d-155">Next Steps</span></span>
<span data-ttu-id="ea41d-156">Agora que você aprendeu as noções básicas sobre as filas do Barramento de Serviço, veja [Filas, tópicos e assinaturas][Queues, topics, and subscriptions] para saber mais.</span><span class="sxs-lookup"><span data-stu-id="ea41d-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="ea41d-157">Para obter mais informações, consulte o [Centro de desenvolvedores do Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="ea41d-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
