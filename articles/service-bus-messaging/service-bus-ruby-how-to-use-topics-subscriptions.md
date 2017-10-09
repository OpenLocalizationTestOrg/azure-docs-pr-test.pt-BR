---
title: "tópicos do barramento de serviço do aaaHow toouse (Ruby) | Microsoft Docs"
description: "Saiba como toouse Service Bus tópicos e assinaturas no Azure. Exemplos de código são escritos para aplicativos Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Como toouse Service Bus tópicos e assinaturas com Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artigo descreve como toouse Service Bus tópicos e assinaturas de aplicativos Ruby. Olá cenários abordados incluem **criando tópicos e assinaturas, criando filtros de assinatura, enviando mensagens** tooa tópico **receber mensagens de uma assinatura**, e  **excluir tópicos e assinaturas**. Para obter mais informações sobre os tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Criar um tópico
Olá **Azure::ServiceBusService** objeto permite que você toowork com tópicos. Olá código a seguir cria um **Azure::ServiceBusService** objeto. toocreate um tópico, use Olá `create_topic()` método. saudação de exemplo a seguir cria um tópico ou imprime erros Olá se houver.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Você também pode passar um **Azure::ServiceBus::Topic** objeto com opções adicionais, que permitem que você toooverride configurações do tópico como tamanho de fila toolive ou máximo de tempo de mensagem. Olá exemplo a seguir mostra definindo o máximo da fila Olá too5 GB de tamanho e too1 toolive minutos de tempo:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Criar assinaturas
Assinaturas de tópico também são criadas com hello **Azure::ServiceBusService** objeto. As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.

Assinaturas são persistentes e continuarão tooexist até a eles ou hello tópico eles estão associados são excluídos. Se seu aplicativo contiver lógica toocreate uma assinatura, deve primeiro verificar se a assinatura de saudação já existe usando o método de getSubscription hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma assinatura com o filtro saudação padrão (MatchAll)
Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada. Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello. Olá, exemplo a seguir cria uma assinatura chamada "todas as mensagens" e usa Olá padrão **MatchAll** filtro.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Criar assinaturas com os filtros
Você também pode definir filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve ser exibidas dentro de uma assinatura específica.

Olá, mais flexível tipo de filtro de assinaturas com suporte é Olá **Azure::ServiceBus::SqlFilter**, que implementa um subconjunto do SQL92. Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico. Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [SqlFilter](service-bus-messaging-sql-filter.md) sintaxe.

Você pode adicionar filtros tooa assinatura usando Olá `create_rule()` método hello **Azure::ServiceBusService** objeto. Esse método permite que você tooadd novos filtros tooan assinatura existente.

Desde o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou Olá **MatchAll** substituirá os outros filtros que você pode especificar. Você pode remover a regra padrão de saudação usando Olá `delete_rule()` método hello **Azure::ServiceBusService** objeto.

Olá, exemplo a seguir cria uma assinatura chamada "mensagens de alta" com um **Azure::ServiceBus::SqlFilter** que seleciona somente as mensagens que têm um personalizado `message_number` propriedade maior que 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `low-messages` com um **Azure::ServiceBus::SqlFilter** que seleciona somente as mensagens que têm um `message_number` propriedade menor ou igual too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Quando uma mensagem agora é enviada muito`test-topic`, sempre será entregue tooreceivers inscrito toohello `all-messages` assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello `high-messages` e `low-messages` (de assinaturas de tópico Dependendo de conteúdo da mensagem de saudação).

## <a name="send-messages-tooa-topic"></a>Enviar tópico tooa de mensagens
toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar Olá `send_topic_message()` método hello **Azure::ServiceBusService** objeto. As mensagens enviadas tooService tópicos do barramento são instâncias da saudação **Azure::ServiceBus::BrokeredMessage** objetos. **Azure::ServiceBus::BrokeredMessage** objetos têm um conjunto de propriedades padrão (como `label` e `time_to_live`), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados de cadeia de caracteres. Um aplicativo pode definir o corpo de saudação da mensagem de saudação passando um toohello de valor de cadeia de caracteres `send_topic_message()` método e qualquer necessário propriedades padrão serão preenchidas por valores padrão.

Olá exemplo a seguir demonstra como teste toosend cinco mensagens muito`test-topic`. Observe que Olá `message_number` valor da propriedade personalizada de cada mensagem varia em iteração de saudação do loop de saudação (Isso determina qual assinatura recebe):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico. O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma assinatura
As mensagens são recebidas de uma assinatura usando Olá `receive_subscription_message()` método hello **Azure::ServiceBusService** objeto. Por padrão, as mensagens são read(peak) e bloqueado sem excluí-la da assinatura de saudação. Você pode ler e excluir mensagem de saudação de assinatura Olá Olá configuração `peek_lock` opção muito**false**.

comportamento padrão de saudação torna Olá ler e excluir uma operação de duas etapas, que também torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `delete_subscription_message()` método e fornecendo toobe de mensagem de saudação excluído como um parâmetro. Olá `delete_subscription_message()` método será marcar a mensagem de saudação como sendo consumida e removê-lo da assinatura de saudação.

Se hello `:peek_lock` parâmetro está definido muito**false**, ler e excluir a mensagem de saudação torna-se o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processar uma mensagem no evento de saudação de um Falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando `receive_subscription_message()`. exemplo Hello primeiro recebe e exclui uma mensagem de saudação `low-messages` assinatura usando `:peek_lock` definido muito**false**, em seguida, ele recebe outra mensagem de saudação `high-messages` e, em seguida, exclui hello usando `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlock_subscription_message()` método hello **Azure::ServiceBusService** objeto. Isso faz com que saudação do barramento de serviço toounlock mensagem de assinatura do hello e torná-lo disponível toobe recebida novamente, ou por Olá mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em assinatura hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `delete_subscription_message()` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *, pelo menos, após processamento*; ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Essa lógica geralmente é obtida usando Olá `message_id` propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Excluir tópicos e assinaturas
Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente. exemplo Hello abaixo demonstra como o tópico de saudação toodelete nomeados `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Excluir um tópico também exclui qualquer assinatura que é registrada com o tópico de saudação. As assinaturas também podem ser excluídas de forma independente. Olá código a seguir demonstra como assinatura de saudação toodelete nomeados `high-messages` de saudação `test-topic` tópico:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.

* Confira [Filas, tópicos e assinaturas](service-bus-queues-topics-subscriptions.md).
* Referência da API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Visite Olá [SDK do Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositório no GitHub.

[Azure portal]: https://portal.azure.com
