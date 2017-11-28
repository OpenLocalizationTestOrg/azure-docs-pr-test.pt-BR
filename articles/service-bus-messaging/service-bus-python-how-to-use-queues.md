---
title: aaaHow toouse Azure Service Bus filas com Python | Microsoft Docs
description: Saiba como toouse Azure Service Bus filas do Python.
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="3286f-103">Como toouse Service Bus filas com Python</span><span class="sxs-lookup"><span data-stu-id="3286f-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3286f-104">Este artigo descreve como as filas do barramento de serviço toouse.</span><span class="sxs-lookup"><span data-stu-id="3286f-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="3286f-105">exemplos de saudação são escritos em Python e usar Olá [pacote do barramento de serviço do Azure Python][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="3286f-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="3286f-106">Olá cenários abordados incluem **Criando filas, enviando e recebendo mensagens**, e **excluindo filas**.</span><span class="sxs-lookup"><span data-stu-id="3286f-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="3286f-107">tooinstall Python ou hello [pacote do barramento de serviço do Azure Python][Python Azure Service Bus package], consulte Olá [guia de instalação do Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="3286f-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="3286f-108">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="3286f-108">Create a queue</span></span>
<span data-ttu-id="3286f-109">Olá **ServiceBusService** objeto permite que você toowork com filas.</span><span class="sxs-lookup"><span data-stu-id="3286f-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="3286f-110">Adicione Olá código superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically barramento de serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="3286f-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="3286f-111">Olá código a seguir cria um **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="3286f-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="3286f-112">Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace, nome da chave e valor da SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="3286f-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="3286f-113">Olá valores de nome de chave de SAS hello e valor podem ser encontrados no hello [portal do Azure] [ Azure portal] informações de conexão, ou no Visual Studio de saudação **propriedades** painel ao selecionar Olá namespace do barramento de serviço no Gerenciador de servidores (conforme mostrado na seção anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="3286f-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="3286f-114">Olá `create_queue` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações de fila padrão como o tempo da mensagem toolive (TTL) ou o tamanho máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="3286f-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="3286f-115">Olá exemplo a seguir define Olá máximo da fila tamanho too5 GB e minuto de too1 de valor TTL hello:</span><span class="sxs-lookup"><span data-stu-id="3286f-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="3286f-116">Mensagens tooa fila de envio</span><span class="sxs-lookup"><span data-stu-id="3286f-116">Send messages tooa queue</span></span>
<span data-ttu-id="3286f-117">toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `send_queue_message` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="3286f-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="3286f-118">Olá exemplo a seguir demonstra como toosend uma fila de toohello de mensagens de teste chamado `taskqueue` usando `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="3286f-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="3286f-119">Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3286f-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3286f-120">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="3286f-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3286f-121">Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="3286f-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="3286f-122">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="3286f-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="3286f-123">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="3286f-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3286f-124">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="3286f-124">Receive messages from a queue</span></span>
<span data-ttu-id="3286f-125">As mensagens são recebidas de uma fila usando Olá `receive_queue_message` método hello **ServiceBusService** objeto:</span><span class="sxs-lookup"><span data-stu-id="3286f-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="3286f-126">As mensagens serão excluídas da fila de saudação conforme elas são de leitura quando Olá parâmetro `peek_lock` está definido muito**False**.</span><span class="sxs-lookup"><span data-stu-id="3286f-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="3286f-127">Você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro de saudação configuração `peek_lock` muito**True**.</span><span class="sxs-lookup"><span data-stu-id="3286f-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="3286f-128">Olá comportamento de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="3286f-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="3286f-129">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="3286f-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="3286f-130">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="3286f-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="3286f-131">Se hello `peek_lock` parâmetro está definido muito**True**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="3286f-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3286f-132">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3286f-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="3286f-133">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber processo por chamada hello **excluir** método hello **mensagem** objeto.</span><span class="sxs-lookup"><span data-stu-id="3286f-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="3286f-134">Olá **excluir** método será marcar a mensagem de saudação como sendo consumida e removê-la da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="3286f-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3286f-135">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="3286f-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="3286f-136">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="3286f-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3286f-137">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **desbloquear** método hello **mensagem** objeto.</span><span class="sxs-lookup"><span data-stu-id="3286f-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="3286f-138">Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="3286f-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3286f-139">Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se Olá falha de aplicativo hello tooprocess Olá mensagem antes de tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="3286f-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="3286f-140">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **excluir** método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="3286f-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="3286f-141">Isso é geralmente chamado **, pelo menos, após processamento**, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="3286f-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="3286f-142">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="3286f-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="3286f-143">Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="3286f-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3286f-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3286f-144">Next steps</span></span>
<span data-ttu-id="3286f-145">Agora que você aprendeu os fundamentos de saudação de filas do barramento de serviço, consulte esses toolearn artigos mais.</span><span class="sxs-lookup"><span data-stu-id="3286f-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="3286f-146">[Filas, tópicos e assinaturas][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="3286f-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

