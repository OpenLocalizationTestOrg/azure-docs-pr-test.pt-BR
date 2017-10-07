---
title: aaaHow toouse Azure Service Bus filas com Ruby | Microsoft Docs
description: "Saiba como filas de toouse barramento de serviço no Azure. Exemplos de códigos escritos em Ruby."
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
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Como toouse Service Bus filas com Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este guia descreve como as filas do barramento de serviço toouse. exemplos de saudação são escritos em Ruby e usam Olá gem do Azure. Olá cenários abordados incluem **Criando filas, enviando e recebendo mensagens**, e **excluindo filas**. Para obter mais informações sobre as filas do barramento de serviço, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Como toocreate uma fila
Olá **Azure::ServiceBusService** objeto permite que você toowork com filas. toocreate uma fila, use Olá `create_queue()` método. Olá exemplo a seguir cria uma fila ou imprime os erros.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

Você também pode passar um **Azure::ServiceBus::Queue** do objeto com opções adicionais, que permite toooverride Olá fila as configurações padrão, como tamanho de fila toolive ou máximo de tempo de mensagem. saudação de exemplo a seguir mostra como tooset Olá GB de too5 de tamanho máximo da fila e too1 toolive minutos de tempo:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Como toosend mensagens de fila de tooa
toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `send_queue_message()` método hello **Azure::ServiceBusService** objeto. Mensagens enviadas muito (e recebidas pelo) barramento de serviço filas são **Azure::ServiceBus::BrokeredMessage** objetos e tem um conjunto de propriedades padrão (como `label` e `time_to_live`), um dicionário que é usado toohold propriedades específicas do aplicativo personalizadas e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir o corpo de saudação da mensagem de saudação, passando um valor de cadeia de caracteres como mensagem de saudação e as propriedades padrão são preenchidas com valores padrão.

Olá exemplo a seguir demonstra como toosend uma fila de toohello de mensagens de teste chamado `test-queue` usando `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação. O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.

## <a name="how-tooreceive-messages-from-a-queue"></a>Como tooreceive mensagens de uma fila
As mensagens são recebidas de uma fila usando Olá `receive_queue_message()` método hello **Azure::ServiceBusService** objeto. Por padrão, mensagens são lidos e bloqueadas sem que sejam excluídas da fila de saudação. No entanto, você pode excluir as mensagens da fila de saudação conforme eles são lidos por configuração Olá `:peek_lock` opção muito**false**.

comportamento padrão de saudação torna Olá ler e excluir uma operação de duas etapas, que também torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `delete_queue_message()` método e fornecendo toobe de mensagem de saudação excluído como um parâmetro. Olá `delete_queue_message()` método será marcar a mensagem de saudação como sendo consumida e removê-la da fila de saudação.

Se hello `:peek_lock` parâmetro está definido muito**false**, ler e excluir a mensagem de saudação torna-se o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processar uma mensagem no evento de saudação de um Falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço marcou a mensagem de saudação como sendo consumida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Olá exemplo a seguir demonstra como tooreceive e processar mensagens usando `receive_queue_message()`. exemplo Hello primeiro recebe e exclui uma mensagem usando `:peek_lock` definido muito**false**, receber outra mensagem e, em seguida, exclui hello usando `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlock_queue_message()` método hello **Azure::ServiceBusService** objeto. Essa chamada faz com que hello de toounlock de barramento de serviço de mensagens na fila de saudação e torná-lo disponível toobe recebida novamente, ou por Olá mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e a mensagem de saudação desbloqueia o barramento de serviço automaticamente e o torna disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `delete_queue_message()` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Esse processo é geralmente chamado *, pelo menos, após processamento*; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá `message_id` propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, siga essas toolearn links mais.

* Visão geral de [filas, tópicos e assinaturas](service-bus-queues-topics-subscriptions.md).
* Visite Olá [SDK do Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositório no GitHub.

Para obter uma comparação entre filas do barramento de serviço do Azure Olá discutidas neste artigo e Azure discutidos Olá [como toouse armazenamento de fila do Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) do artigo, consulte [filas do Azure e filas do Azure Service Bus - comparadas e diferenças](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

