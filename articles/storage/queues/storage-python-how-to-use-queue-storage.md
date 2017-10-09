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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>Como toouse armazenamento de fila do Python
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Azure. exemplos de saudação são escritos em Python e usar Olá [Microsoft Azure Storage SDK para Python]. Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**. Para obter mais informações sobre filas, consulte a seção toohello [próximas etapas].

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Como criar uma fila
Olá **QueueService** objeto permite que você trabalhe com filas. Olá código a seguir cria um **QueueService** objeto. Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically armazenamento do Azure:

```python
from azure.storage.queue import QueueService
```

Olá código a seguir cria um **QueueService** objeto usando a chave de nome e uma conta de conta de armazenamento do hello. Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como inserir uma mensagem em uma fila
tooinsert uma mensagem em uma fila, use Olá **colocar\_mensagem** método para criar uma nova mensagem e adicioná-lo toohello fila.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **inspeção\_mensagens** método. Por padrão, **peek\_messages()** inspeciona uma única mensagem.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Como: remover mensagens da fila
Seu código remove uma mensagem de uma fila em duas etapas. Quando você chama **obter\_mensagens**, obter próxima mensagem de saudação em uma fila por padrão. Uma mensagem retornada de **obter\_mensagens** se torna invisível tooany outro código de leitura de mensagens dessa fila. Por padrão, essa mensagem permanece invisível por 30 segundos. toofinish mensagem de saudação remover da fila hello, você também deve chamar **excluir\_mensagem**. Esse processo de duas etapas de remoção de uma mensagem garante que, quando falha tooprocess uma mensagem devido à falha de hardware ou software no seu código, outra instância do seu código pode obter a mesma mensagem de erro e tente novamente. Seu código chama **excluir\_mensagem** logo depois que a mensagem de saudação foi processada.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Há duas maneiras de personalizar a recuperação da mensagem de uma fila.
Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem. usos de exemplo de código a seguir de saudação do **obter\_mensagens** mensagens tooget 16 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop for. Ele também define o tempo limite de invisibilidade de saudação para cinco minutos para cada mensagem.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação. Se a mensagem representa uma tarefa de trabalho, você pode usar tooupdate esse recurso o status da tarefa de trabalho hello. código de saudação abaixo usa Olá **atualizar\_mensagem** método tooupdate uma mensagem. tempo limite de visibilidade de saudação é definido too0, indicando que a mensagem será exibida imediatamente e Olá conteúdo é atualizado.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Como Obter Olá comprimento da fila
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. O **obter\_fila\_metadados** método pergunta Olá fila serviço tooreturn metadados sobre fila hello e Olá **approximate_message_count**. resultado de Olá só é aproximado, pois mensagens podem ser adicionadas ou removidas depois que o serviço de fila responde tooyour solicitação.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Como excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir\_fila** método.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links mais.

* [Centro de desenvolvedores do Python](/develop/python/)
* [API REST de serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog da equipe de Armazenamento do Azure]
* [Microsoft Azure Storage SDK para Python]

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK para Python]: https://github.com/Azure/azure-storage-python