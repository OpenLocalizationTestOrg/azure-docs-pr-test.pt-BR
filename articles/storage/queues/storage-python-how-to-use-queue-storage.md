---
title: Como usar o Armazenamento de filas do Python | Microsoft Docs
description: "Saiba como usar o serviço Fila do Azure do Python para criar e excluir filas, bem como para inserir, obter e excluir mensagens."
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
ms.openlocfilehash: 963c11acb7939993568a774cd281145a8059b5a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="120c1-103">Como usar o Armazenamento de fila do Python</span><span class="sxs-lookup"><span data-stu-id="120c1-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="120c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="120c1-104">Overview</span></span>
<span data-ttu-id="120c1-105">Este guia mostra como executar cenários comuns usando o serviço de armazenamento de Fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="120c1-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="120c1-106">Os exemplos são escritos em Python e usam o [Microsoft Azure Storage SDK for Python](SDK do Armazenamento do Microsoft Azure para Python).</span><span class="sxs-lookup"><span data-stu-id="120c1-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="120c1-107">Os cenários abrangidos incluem **inserir**, **exibir**, **obter** e **excluir** mensagens da fila, bem como **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="120c1-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="120c1-108">Para obter mais informações sobre filas, consulte a seção [Próximas etapas].</span><span class="sxs-lookup"><span data-stu-id="120c1-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="120c1-109">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="120c1-109">How To: Create a Queue</span></span>
<span data-ttu-id="120c1-110">O objeto **QueueService** permite que você trabalhe com filas.</span><span class="sxs-lookup"><span data-stu-id="120c1-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="120c1-111">O código a seguir cria um objeto **QueueService** .</span><span class="sxs-lookup"><span data-stu-id="120c1-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="120c1-112">Adicione o seguinte próximo à parte superior de qualquer arquivo Python no qual você deseja acessar o Armazenamento do Azure programaticamente:</span><span class="sxs-lookup"><span data-stu-id="120c1-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="120c1-113">O código a seguir cria um objeto **QueueService** usando o nome da conta de armazenamento e a chave da conta.</span><span class="sxs-lookup"><span data-stu-id="120c1-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="120c1-114">Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.</span><span class="sxs-lookup"><span data-stu-id="120c1-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="120c1-115">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="120c1-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="120c1-116">Para inserir uma mensagem em uma fila, use o método **put\_message** para criar uma nova mensagem e adicioná-la à fila.</span><span class="sxs-lookup"><span data-stu-id="120c1-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="120c1-117">Como: espiar a próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="120c1-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="120c1-118">Você pode inspecionar a mensagem na frente de uma fila sem removê-la da fila chamando o método **peek\_messages**.</span><span class="sxs-lookup"><span data-stu-id="120c1-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="120c1-119">Por padrão, **peek\_messages()** inspeciona uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="120c1-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="120c1-120">Como: remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="120c1-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="120c1-121">Seu código remove uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="120c1-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="120c1-122">Ao chamar **get\_messages**, você receberá a próxima mensagem em uma fila por padrão.</span><span class="sxs-lookup"><span data-stu-id="120c1-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="120c1-123">Uma mensagem retornada de **get\_messages** torna-se invisível para todas as outras mensagens de leitura de código da fila.</span><span class="sxs-lookup"><span data-stu-id="120c1-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="120c1-124">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="120c1-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="120c1-125">Para terminar de remover a mensagem da fila, você também deve chamar **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="120c1-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="120c1-126">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="120c1-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="120c1-127">Seu código chama **delete\_message** logo depois que a mensagem é processada.</span><span class="sxs-lookup"><span data-stu-id="120c1-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="120c1-128">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="120c1-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="120c1-129">Primeiro, você pode obter um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="120c1-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="120c1-130">Segundo, você pode definir um tempo limite de invisibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="120c1-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="120c1-131">O seguinte exemplo de código usa o método **get\_messages** para receber 16 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="120c1-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="120c1-132">Em seguida, ele processa cada mensagem usando um loop for.</span><span class="sxs-lookup"><span data-stu-id="120c1-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="120c1-133">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="120c1-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="120c1-134">Como: alterar o conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="120c1-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="120c1-135">Você pode alterar o conteúdo de uma mensagem in-loco na fila.</span><span class="sxs-lookup"><span data-stu-id="120c1-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="120c1-136">Se a mensagem representar uma tarefa de trabalho, você poderá usar esse recurso para atualizar o status da tarefa de trabalho.</span><span class="sxs-lookup"><span data-stu-id="120c1-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="120c1-137">O código a seguir usa o método **update\_message** para atualizar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="120c1-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="120c1-138">O tempo limite de visibilidade está definido como 0, indicando que a mensagem será exibida imediatamente e o conteúdo será atualizado.</span><span class="sxs-lookup"><span data-stu-id="120c1-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="120c1-139">Como obter o comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="120c1-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="120c1-140">Você pode obter uma estimativa do número de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="120c1-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="120c1-141">O método **get\_queue\_metadata** solicita que o serviço Fila retorne os metadados sobre a fila e a **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="120c1-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="120c1-142">O resultado é aproximado apenas porque as mensagens podem ser adicionadas ou removidas depois que o serviço de fila responde à sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="120c1-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="120c1-143">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="120c1-143">How To: Delete a Queue</span></span>
<span data-ttu-id="120c1-144">Para excluir uma fila e todas as mensagens contidas nela, chame o método **delete\_queue**.</span><span class="sxs-lookup"><span data-stu-id="120c1-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="120c1-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="120c1-145">Next Steps</span></span>
<span data-ttu-id="120c1-146">Agora que você aprendeu os conceitos básicos do Armazenamento de Filas, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="120c1-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="120c1-147">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="120c1-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="120c1-148">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="120c1-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="120c1-149">[Blog da equipe de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="120c1-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="120c1-150">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="120c1-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python