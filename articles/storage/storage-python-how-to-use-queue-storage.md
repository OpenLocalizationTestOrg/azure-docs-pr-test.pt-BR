---
title: aaaHow toouse armazenamento de fila do Python | Microsoft Docs
description: "Saiba como toouse Olá serviço de fila do Azure do Python toocreate e excluir filas, inserir, obter e excluir mensagens."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="c2b36-103">Como toouse armazenamento de fila do Python</span><span class="sxs-lookup"><span data-stu-id="c2b36-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c2b36-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c2b36-104">Overview</span></span>
<span data-ttu-id="c2b36-105">Este guia mostra como os cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2b36-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="c2b36-106">exemplos de saudação são escritos em Python e usar Olá [Microsoft Azure Storage SDK para Python].</span><span class="sxs-lookup"><span data-stu-id="c2b36-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="c2b36-107">Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="c2b36-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="c2b36-108">Para obter mais informações sobre filas, consulte a seção toohello [próximas etapas].</span><span class="sxs-lookup"><span data-stu-id="c2b36-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c2b36-109">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-109">How To: Create a Queue</span></span>
<span data-ttu-id="c2b36-110">Olá **QueueService** objeto permite que você trabalhe com filas.</span><span class="sxs-lookup"><span data-stu-id="c2b36-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="c2b36-111">Olá código a seguir cria um **QueueService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c2b36-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="c2b36-112">Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="c2b36-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="c2b36-113">Olá código a seguir cria um **QueueService** objeto usando a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="c2b36-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="c2b36-114">Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.</span><span class="sxs-lookup"><span data-stu-id="c2b36-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c2b36-115">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="c2b36-116">tooinsert uma mensagem em uma fila, use Olá **colocar\_mensagem** método para criar uma nova mensagem e adicioná-lo toohello fila.</span><span class="sxs-lookup"><span data-stu-id="c2b36-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="c2b36-117">Como: Espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="c2b36-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="c2b36-118">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **inspeção\_mensagens** método.</span><span class="sxs-lookup"><span data-stu-id="c2b36-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="c2b36-119">Por padrão, **peek\_messages()** inspeciona uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="c2b36-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="c2b36-120">Como: remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="c2b36-121">Seu código remove uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c2b36-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="c2b36-122">Quando você chama **obter\_mensagens**, obter próxima mensagem de saudação em uma fila por padrão.</span><span class="sxs-lookup"><span data-stu-id="c2b36-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="c2b36-123">Uma mensagem retornada de **obter\_mensagens** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="c2b36-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="c2b36-124">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="c2b36-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="c2b36-125">toofinish mensagem de saudação remover da fila hello, você também deve chamar **excluir\_mensagem**.</span><span class="sxs-lookup"><span data-stu-id="c2b36-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="c2b36-126">Esse processo de duas etapas de remoção de uma mensagem garante que, quando falha tooprocess uma mensagem devido à falha de hardware ou software no seu código, outra instância do seu código pode obter a mesma mensagem de erro e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="c2b36-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c2b36-127">Seu código chama **excluir\_mensagem** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="c2b36-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="c2b36-128">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="c2b36-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="c2b36-129">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="c2b36-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="c2b36-130">Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="c2b36-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="c2b36-131">usos de exemplo de código a seguir de saudação do **obter\_mensagens** mensagens tooget 16 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="c2b36-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="c2b36-132">Em seguida, ele processa cada mensagem usando um loop for.</span><span class="sxs-lookup"><span data-stu-id="c2b36-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="c2b36-133">Ele também define o tempo limite de invisibilidade de saudação para cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="c2b36-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="c2b36-134">Como: Alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="c2b36-135">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2b36-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="c2b36-136">Se a mensagem representa uma tarefa de trabalho, você pode usar tooupdate esse recurso o status da tarefa de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="c2b36-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="c2b36-137">código de saudação abaixo usa Olá **atualizar\_mensagem** método tooupdate uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="c2b36-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="c2b36-138">tempo limite de visibilidade de saudação é definido too0, indicando que a mensagem será exibida imediatamente e Olá conteúdo é atualizado.</span><span class="sxs-lookup"><span data-stu-id="c2b36-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="c2b36-139">Como Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="c2b36-140">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="c2b36-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="c2b36-141">O **obter\_fila\_metadados** método pergunta Olá fila serviço tooreturn metadados sobre fila hello e Olá **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="c2b36-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="c2b36-142">resultado de Olá só é aproximado, pois mensagens podem ser adicionadas ou removidas depois que o serviço de fila responde tooyour solicitação.</span><span class="sxs-lookup"><span data-stu-id="c2b36-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c2b36-143">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="c2b36-143">How To: Delete a Queue</span></span>
<span data-ttu-id="c2b36-144">toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir\_fila** método.</span><span class="sxs-lookup"><span data-stu-id="c2b36-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="c2b36-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2b36-145">Next Steps</span></span>
<span data-ttu-id="c2b36-146">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="c2b36-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="c2b36-147">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="c2b36-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="c2b36-148">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c2b36-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="c2b36-149">[Blog da equipe de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="c2b36-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="c2b36-150">[Microsoft Azure Storage SDK para Python]</span><span class="sxs-lookup"><span data-stu-id="c2b36-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK para Python]: https://github.com/Azure/azure-storage-python