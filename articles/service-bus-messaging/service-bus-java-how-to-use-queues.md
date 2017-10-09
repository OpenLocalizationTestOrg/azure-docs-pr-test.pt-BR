---
title: "filas de aaaHow toouse barramento de serviço do Azure com Java | Microsoft Docs"
description: "Saiba como filas de toouse barramento de serviço no Azure. Exemplos de códigos escritos em Java."
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
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="8c4dd-104">Como toouse Service Bus filas com Java</span><span class="sxs-lookup"><span data-stu-id="8c4dd-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="8c4dd-105">Este artigo descreve como as filas do barramento de serviço toouse.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="8c4dd-106">exemplos de saudação são escritos em Java e usam Olá [SDK do Azure para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="8c4dd-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="8c4dd-107">Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="8c4dd-108">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8c4dd-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="8c4dd-109">Verifique se você instalou Olá [SDK do Azure para Java] [ Azure SDK for Java] antes de compilar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="8c4dd-110">Se você estiver usando o Eclipse, você pode instalar Olá [Kit de ferramentas do Azure para Eclipse] [ Azure Toolkit for Eclipse] que inclui Olá SDK do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="8c4dd-111">Você pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="8c4dd-112">Adicione o seguinte Olá `import` superior de toohello instruções saudação do arquivo de Java:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="8c4dd-113">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="8c4dd-113">Create a queue</span></span>
<span data-ttu-id="8c4dd-114">Operações de gerenciamento para as filas do Barramento de Serviço podem ser realizadas pela classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="8c4dd-115">Um **ServiceBusContract** objeto for construído com uma configuração apropriada que encapsula o token SAS com toomanage de permissões e hello **ServiceBusContract** classe é um ponto único de saudação de comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="8c4dd-116">Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e excluir filas.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="8c4dd-117">Olá como o exemplo a seguir mostra um **ServiceBusService** objeto pode ser usado toocreate uma fila denominada `TestQueue`, com um namespace chamado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

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

<span data-ttu-id="8c4dd-118">Há métodos no `QueueInfo` que permitem que propriedades de saudação fila toobe ajustadas (por exemplo: tooset saudação padrão time-to-live (TTL) valor toobe aplicada toomessages enviados toohello fila).</span><span class="sxs-lookup"><span data-stu-id="8c4dd-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="8c4dd-119">Olá exemplo a seguir mostra como toocreate uma fila denominada `TestQueue` com um tamanho máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="8c4dd-120">Observe que você pode usar o hello `listQueues` método **ServiceBusContract** objetos toocheck se já existe uma fila com um nome especificado em um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="8c4dd-121">Mensagens tooa fila de envio</span><span class="sxs-lookup"><span data-stu-id="8c4dd-121">Send messages tooa queue</span></span>
<span data-ttu-id="8c4dd-122">toosend uma fila de barramento de serviço tooa mensagens, o aplicativo obtém um **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="8c4dd-123">Olá mostrado no código a seguir como toosend uma mensagem de saudação `TestQueue` fila criada anteriormente no hello `HowToSample` namespace:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

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

<span data-ttu-id="8c4dd-124">As mensagens enviadas para e recebidas do barramento de serviço filas são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="8c4dd-125">[BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de propriedades padrão (como [rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é usado toohold personalizado propriedades específicas do aplicativo e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="8c4dd-126">Um aplicativo pode definir o corpo de saudação da mensagem de saudação passando qualquer objeto serializável para construtor de saudação do hello [BrokeredMessage][BrokeredMessage], e o serializador adequado Olá será usado objeto de saudação tooserialize.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="8c4dd-127">Como alternativa, você pode fornecer um objeto **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="8c4dd-128">Olá exemplo a seguir demonstra como teste toosend cinco mensagens toothe `TestQueue` **MessageSender** obtivemos no trecho de código anterior hello:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="8c4dd-129">Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="8c4dd-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="8c4dd-130">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="8c4dd-131">Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="8c4dd-132">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="8c4dd-133">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="8c4dd-133">Receive messages from a queue</span></span>
<span data-ttu-id="8c4dd-134">mensagens de tooreceive Olá principal forma de uma fila é toouse uma **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="8c4dd-135">As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="8c4dd-136">Ao usar o hello **ReceiveAndDelete** modo, recebe é uma operação de captura único - ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma fila, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="8c4dd-137">**ReceiveAndDelete** modo (que é o modo padrão de saudação) é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processar uma mensagem em caso de saudação de uma falha.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="8c4dd-138">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="8c4dd-139">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="8c4dd-140">Em **PeekLock** , modo de recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="8c4dd-141">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="8c4dd-142">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando **excluir** na mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="8c4dd-143">Quando o Service Bus vê Olá **excluir** chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="8c4dd-144">Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando **PeekLock** modo (não o modo padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="8c4dd-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="8c4dd-145">Olá exemplo a seguir faz um loop infinito e processa as mensagens que chegam em nosso `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="8c4dd-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

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
            // Display hello queue message.
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
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="8c4dd-146">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="8c4dd-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="8c4dd-147">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="8c4dd-148">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **unlockMessage** método na mensagem recebida (em vez da saudação **deleteMessage** método).</span><span class="sxs-lookup"><span data-stu-id="8c4dd-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="8c4dd-149">Isso faz com que hello de toounlock de barramento de serviço de mensagens na fila de saudação e torná-lo disponível toobe recebida novamente, ou por Olá mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="8c4dd-150">Também há um tempo limite associado a uma mensagem bloqueada na fila, e se o aplicativo hello falha tooprocess Olá mensagem antes do tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloqueia a mensagem de saudação automaticamente e torna disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="8c4dd-151">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **deleteMessage** solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="8c4dd-152">Isso é geralmente chamado *, pelo menos, após processamento*; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="8c4dd-153">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="8c4dd-154">Isso geralmente é obtido usando Olá **getMessageId** método de mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c4dd-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c4dd-155">Next Steps</span></span>
<span data-ttu-id="8c4dd-156">Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8c4dd-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="8c4dd-157">Para obter mais informações, consulte Olá [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="8c4dd-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
