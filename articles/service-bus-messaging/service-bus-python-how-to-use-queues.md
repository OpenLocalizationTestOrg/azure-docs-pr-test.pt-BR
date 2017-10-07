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
# <a name="how-toouse-service-bus-queues-with-python"></a>Como toouse Service Bus filas com Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artigo descreve como as filas do barramento de serviço toouse. exemplos de saudação são escritos em Python e usar Olá [pacote do barramento de serviço do Azure Python][Python Azure Service Bus package]. Olá cenários abordados incluem **Criando filas, enviando e recebendo mensagens**, e **excluindo filas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python ou hello [pacote do barramento de serviço do Azure Python][Python Azure Service Bus package], consulte Olá [guia de instalação do Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Criar uma fila
Olá **ServiceBusService** objeto permite que você toowork com filas. Adicione Olá código superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically barramento de serviço a seguir:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Olá código a seguir cria um **ServiceBusService** objeto. Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace, nome da chave e valor da SAS (Assinatura de Acesso Compartilhado).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Olá valores de nome de chave de SAS hello e valor podem ser encontrados no hello [portal do Azure] [ Azure portal] informações de conexão, ou no Visual Studio de saudação **propriedades** painel ao selecionar Olá namespace do barramento de serviço no Gerenciador de servidores (conforme mostrado na seção anterior Olá).

```python
bus_service.create_queue('taskqueue')
```

Olá `create_queue` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações de fila padrão como o tempo da mensagem toolive (TTL) ou o tamanho máximo da fila. Olá exemplo a seguir define Olá máximo da fila tamanho too5 GB e minuto de too1 de valor TTL hello:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Mensagens tooa fila de envio
toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `send_queue_message` método hello **ServiceBusService** objeto.

Olá exemplo a seguir demonstra como toosend uma fila de toohello de mensagens de teste chamado `taskqueue` usando `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação. O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB. Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).

## <a name="receive-messages-from-a-queue"></a>Receber mensagens de uma fila
As mensagens são recebidas de uma fila usando Olá `receive_queue_message` método hello **ServiceBusService** objeto:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

As mensagens serão excluídas da fila de saudação conforme elas são de leitura quando Olá parâmetro `peek_lock` está definido muito**False**. Você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro de saudação configuração `peek_lock` muito**True**.

Olá comportamento de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Se hello `peek_lock` parâmetro está definido muito**True**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber processo por chamada hello **excluir** método hello **mensagem** objeto. Olá **excluir** método será marcar a mensagem de saudação como sendo consumida e removê-la da fila de saudação.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **desbloquear** método hello **mensagem** objeto. Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se Olá falha de aplicativo hello tooprocess Olá mensagem antes de tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **excluir** método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado **, pelo menos, após processamento**, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu os fundamentos de saudação de filas do barramento de serviço, consulte esses toolearn artigos mais.

* [Filas, tópicos e assinaturas][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

