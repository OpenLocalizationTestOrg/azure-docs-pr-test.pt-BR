---
title: "Como usar as filas de Barramento de Serviço do Azure com Python | Microsoft Docs"
description: "Saiba como usar as filas do barramento de serviço do Azure do Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="324ad-103">Como usar filas do Barramento de Serviço com Python</span><span class="sxs-lookup"><span data-stu-id="324ad-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="324ad-104">Este artigo descreve como usar as filas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="324ad-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="324ad-105">Os exemplos são escritos em Python e usam o [pacote de Barramento de Serviço do Azure para Python][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="324ad-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="324ad-106">Os cenários cobertos incluem **criar filas, enviar e receber mensagens** e **excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="324ad-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="324ad-107">Para instalar o Python ou o [pacote do Barramento de Serviço do Azure para Python][Python Azure Service Bus package], veja o [Guia de instalação do Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="324ad-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="324ad-108">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="324ad-108">Create a queue</span></span>
<span data-ttu-id="324ad-109">O objeto **ServiceBusService** permite que você trabalhe com filas.</span><span class="sxs-lookup"><span data-stu-id="324ad-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="324ad-110">Adicione o seguinte código próximo à parte superior de qualquer arquivo Python no qual você deseja acessar o Barramento de Serviço de forma programática:</span><span class="sxs-lookup"><span data-stu-id="324ad-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="324ad-111">O código a seguir cria um objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="324ad-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="324ad-112">Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace, nome da chave e valor da SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="324ad-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="324ad-113">Os valores para o nome chave e valor da SAS podem ser encontrados na informação de conexão do [Portal do Azure][Azure portal] ou no painel das **Propriedades** do Visual Studio ao selecionar o namespace do Barramento de Serviço no Gerenciador de Servidores (conforme mostrado na seção anterior).</span><span class="sxs-lookup"><span data-stu-id="324ad-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="324ad-114">O método `create_queue` também dá suporte para opções adicionais, que permitem a substituição de configurações padrão da fila, como a vida útil (TTL) da mensagem ou o tamanho máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="324ad-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="324ad-115">O exemplo a seguir define o tamanho máximo da fila como 5 GB e o valor de TTL como um minuto:</span><span class="sxs-lookup"><span data-stu-id="324ad-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="324ad-116">Enviar mensagens a uma fila</span><span class="sxs-lookup"><span data-stu-id="324ad-116">Send messages to a queue</span></span>
<span data-ttu-id="324ad-117">Para enviar uma mensagem para uma fila do Barramento de Serviço, seu aplicativo chamará o método `send_queue_message` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="324ad-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="324ad-118">O exemplo a seguir demonstra como enviar uma mensagem de teste à fila chamada `taskqueue` usando `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="324ad-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="324ad-119">As filas do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="324ad-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="324ad-120">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="324ad-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="324ad-121">Não há nenhum limite no número de mensagens mantidas em uma fila mas há uma capacidade do tamanho total das mensagens mantidas por uma fila.</span><span class="sxs-lookup"><span data-stu-id="324ad-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="324ad-122">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="324ad-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="324ad-123">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="324ad-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="324ad-124">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="324ad-124">Receive messages from a queue</span></span>
<span data-ttu-id="324ad-125">As mensagens são recebidas de uma fila usando o método `receive_queue_message` no objeto **ServiceBusService**:</span><span class="sxs-lookup"><span data-stu-id="324ad-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="324ad-126">As mensagens são excluídas da fila conforme são lidas quando o parâmetro `peek_lock` é definido como **False**.</span><span class="sxs-lookup"><span data-stu-id="324ad-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="324ad-127">Você pode ler (espiar) e bloquear a mensagem sem excluí-la da fila ao definir o parâmetro `peek_lock` como **True**.</span><span class="sxs-lookup"><span data-stu-id="324ad-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="324ad-128">O comportamento da leitura e da exclusão da mensagem como parte da operação de recebimento é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo possa tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="324ad-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="324ad-129">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="324ad-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="324ad-130">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="324ad-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="324ad-131">Se o parâmetro `peek_lock` estiver definido como **True**, o processo de recebimento se torna uma operação de duas etapas, o que torna possível o suporte a aplicativos que não toleram mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="324ad-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="324ad-132">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="324ad-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="324ad-133">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para processamento futuro), ele conclui a segunda etapa do processo de recebimento chamando o método **delete** no objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="324ad-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="324ad-134">O método **delete** marcará a mensagem como tendo sido consumida e a removerá da fila.</span><span class="sxs-lookup"><span data-stu-id="324ad-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="324ad-135">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="324ad-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="324ad-136">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="324ad-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="324ad-137">Se um aplicativo receptor não conseguir processar a mensagem por algum motivo, ele chamará o método **unlock** no objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="324ad-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="324ad-138">Isso fará com que o Service Bus desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="324ad-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="324ad-139">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se o aplicativo não conseguir processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, em caso de falha do aplicativo), o Service Bus desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="324ad-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="324ad-140">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método **delete** seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="324ad-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="324ad-141">Isso é frequentemente chamado de **Processamento de pelo menos uma vez**, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="324ad-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="324ad-142">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="324ad-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="324ad-143">Isso geralmente é obtido com a propriedade **MessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="324ad-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="324ad-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="324ad-144">Next steps</span></span>
<span data-ttu-id="324ad-145">Agora que você já aprendeu sobre as noções básicas das filas do Barramento de Serviço, confira estes artigo para saber mais.</span><span class="sxs-lookup"><span data-stu-id="324ad-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="324ad-146">[Filas, tópicos e assinaturas][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="324ad-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

