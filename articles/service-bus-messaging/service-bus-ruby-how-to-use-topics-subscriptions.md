---
title: "Como usar os tópicos de Barramento de Serviço (Ruby) | Microsoft Docs"
description: "Aprenda a usar assinaturas e tópicos do Barramento de Serviço no Azure. Exemplos de código são escritos para aplicativos Ruby."
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
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="1e083-104">Como usar tópicos e assinaturas do Barramento de Serviço com Ruby</span><span class="sxs-lookup"><span data-stu-id="1e083-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="1e083-105">Este artigo descreve como usar tópicos do Barramento de Serviço e assinaturas de aplicativos Ruby.</span><span class="sxs-lookup"><span data-stu-id="1e083-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="1e083-106">Os cenários abordados incluem a **criação de tópicos e assinaturas, a criação de filtros de assinatura, o envio de mensagens** para um tópico, o **recebimento de mensagens de uma assinatura** e a **exclusão de tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="1e083-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="1e083-107">Para obter mais informações sobre tópicos e assinaturas, consulte a seção [Próximas etapas](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="1e083-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="1e083-108">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="1e083-108">Create a topic</span></span>
<span data-ttu-id="1e083-109">O objeto **Azure::ServiceBusService** permite que você trabalhe com tópicos.</span><span class="sxs-lookup"><span data-stu-id="1e083-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="1e083-110">O código a seguir cria um objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-111">Para criar um tópico, use o método `create_topic()`.</span><span class="sxs-lookup"><span data-stu-id="1e083-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="1e083-112">O exemplo a seguir cria um tópico ou imprime os erros, caso haja algum.</span><span class="sxs-lookup"><span data-stu-id="1e083-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="1e083-113">Você também pode informar um objeto **Azure::ServiceBus::Topic** com opções adicionais, que permitem a substituição de configurações padrão do tópico como a vida útil da mensagem ou o tamanho máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="1e083-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="1e083-114">O exemplo a seguir mostra a configuração do tamanho máximo da fila para 5 GB e a vida útil para 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="1e083-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="1e083-115">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="1e083-115">Create subscriptions</span></span>
<span data-ttu-id="1e083-116">As assinaturas do tópico também são criadas com o objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-117">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de mensagens entregues à fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1e083-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="1e083-118">As assinaturas são persistentes e continuarão existindo até que elas ou o tópico ao qual estão associadas sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="1e083-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="1e083-119">Se seu aplicativo contiver a lógica para criar uma assinatura, ele deve primeiro verificar se a assinatura já existe usando o método getSubscription.</span><span class="sxs-lookup"><span data-stu-id="1e083-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="1e083-120">Criar uma assinatura com o filtro padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="1e083-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="1e083-121">O filtro **MatchAll** será o padrão usado se nenhum filtro for especificado quando uma nova assinatura for criada.</span><span class="sxs-lookup"><span data-stu-id="1e083-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="1e083-122">Quando o filtro **MatchAll** é usado, todas as mensagens publicadas no tópico são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1e083-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="1e083-123">O exemplo a seguir cria uma assinatura denominada "all-messages" e usa o filtro padrão **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="1e083-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="1e083-124">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="1e083-124">Create subscriptions with filters</span></span>
<span data-ttu-id="1e083-125">Você também pode definir filtros que permitem especificar quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="1e083-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="1e083-126">O tipo de filtro mais flexível com suporte pelas assinaturas é o **Azure::ServiceBus::SqlFilter**, que implementa um subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="1e083-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="1e083-127">Os filtros SQL operam nas propriedades das mensagens que são publicadas no tópico.</span><span class="sxs-lookup"><span data-stu-id="1e083-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="1e083-128">Para obter mais detalhes sobre as expressões que podem ser usadas com um filtro SQL, examine a sintaxe [SqlFilter](service-bus-messaging-sql-filter.md).</span><span class="sxs-lookup"><span data-stu-id="1e083-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="1e083-129">É possível adicionar filtros a uma assinatura usando o método `create_rule()` do objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-130">Este método permite que você adicione novos filtros a uma assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="1e083-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="1e083-131">Como o filtro padrão é aplicado automaticamente em todas as assinaturas novas, você deve primeiro remover o filtro padrão, ou o filtro **MatchAll** substituirá todos os outros filtros que você possa especificar.</span><span class="sxs-lookup"><span data-stu-id="1e083-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="1e083-132">Você pode remover a regra padrão usando o método `delete_rule()` do objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="1e083-133">O exemplo a seguir cria uma assinatura chamada "high-messages" com um **Azure::ServiceBus::SqlFilter** que seleciona apenas mensagens que têm uma propriedade `message_number` personalizada maior que 3:</span><span class="sxs-lookup"><span data-stu-id="1e083-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="1e083-134">Da mesma forma, o seguinte exemplo cria uma assinatura denominada `low-messages` com um **Azure::ServiceBus::SqlFilter** que seleciona apenas mensagens que têm uma propriedade `message_number` menor ou igual a 3:</span><span class="sxs-lookup"><span data-stu-id="1e083-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

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

<span data-ttu-id="1e083-135">Quando uma mensagem é agora enviada para `test-topic`, sempre será entregue aos destinatários inscritos na assinatura do tópico `all-messages` e entregue de forma seletiva aos destinatários inscritos nas assinaturas do tópico `high-messages` e `low-messages` (dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="1e083-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="1e083-136">Enviar mensagens para um tópico</span><span class="sxs-lookup"><span data-stu-id="1e083-136">Send messages to a topic</span></span>
<span data-ttu-id="1e083-137">Para enviar uma mensagem a um tópico do Barramento de Serviço, o aplicativo deve usar o método `send_topic_message()` do objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-138">As mensagens enviadas aos tópicos do Barramento de Serviço são instâncias dos objetos **Azure::ServiceBus::BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="1e083-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="1e083-139">Os objetos **Azure::ServiceBus::BrokeredMessage** têm um conjunto de propriedades padrão (como `label` e `time_to_live`), um dicionário que é usado para manter propriedades personalizadas específicas ao aplicativo e um corpo de dados da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e083-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="1e083-140">Um aplicativo pode definir o corpo da mensagem transmitindo um valor da cadeia ao método `send_topic_message()` e todas as propriedades padrão exigidas serão preenchidas por valores padrão.</span><span class="sxs-lookup"><span data-stu-id="1e083-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="1e083-141">O exemplo a seguir demonstra como enviar cinco mensagens de teste para `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="1e083-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="1e083-142">Observe que o valor da propriedade personalizada `message_number` de cada mensagem varia de acordo com a iteração do loop (isso determina qual assinatura o recebe):</span><span class="sxs-lookup"><span data-stu-id="1e083-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="1e083-143">Os tópicos do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1e083-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1e083-144">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1e083-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1e083-145">Não há nenhum limite no número de mensagens mantidas em um tópico, mas há uma capacidade do tamanho total das mensagens mantidas por um tópico.</span><span class="sxs-lookup"><span data-stu-id="1e083-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="1e083-146">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1e083-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="1e083-147">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="1e083-147">Receive messages from a subscription</span></span>
<span data-ttu-id="1e083-148">As mensagens são recebidas de uma assinatura usando o método `receive_subscription_message()` no objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-149">Por padrão, as mensagens são lidas (pico) e bloqueadas sem excluí-las da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1e083-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="1e083-150">Você pode ler e excluir a mensagem da assinatura definindo a opção `peek_lock` como **false**.</span><span class="sxs-lookup"><span data-stu-id="1e083-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="1e083-151">O comportamento padrão faz com que a leitura e a exclusão se dividam em uma operação de dois estágios, o que também torna possível o suporte a aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="1e083-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1e083-152">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e083-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1e083-153">Depois que o aplicativo termina de processar a mensagem (ou a armazena de forma segura para um processamento futuro), ele conclui o segundo estágio do processo de recebimento, chamando o método `delete_subscription_message()` e fornecendo a mensagem a ser excluída como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1e083-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="1e083-154">O método `delete_subscription_message()` marcará a mensagem como tendo sido consumida e a removerá da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1e083-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="1e083-155">Se o parâmetro `:peek_lock` estiver definido como **false**, a leitura e a exclusão da mensagem se tornam o modelo mais simples e funcionam melhor em cenários nos quais o aplicativo pode tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="1e083-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1e083-156">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="1e083-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1e083-157">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="1e083-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1e083-158">O exemplo a seguir demonstra como as mensagens podem ser recebidas e processadas usando o modo `receive_subscription_message()` padrão.</span><span class="sxs-lookup"><span data-stu-id="1e083-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="1e083-159">O exemplo primeiro recebe e exclui uma mensagem da assinatura `low-messages` usando `:peek_lock` definido como **false**, então recebe outra mensagem do `high-messages` e exclui a mensagem usando `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="1e083-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1e083-160">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="1e083-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="1e083-161">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="1e083-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1e083-162">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele chamará o método `unlock_subscription_message()` no objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1e083-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1e083-163">Isso fará com que o Barramento de Serviço desbloqueie a mensagem na assinatura e disponibilize-a para ser recebida novamente, pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="1e083-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1e083-164">Também há um tempo limite associado a uma mensagem bloqueada na assinatura, e se o aplicativo falhar em processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, se o aplicativo falhar), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="1e083-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="1e083-165">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método `delete_subscription_message()` seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="1e083-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="1e083-166">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="1e083-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1e083-167">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="1e083-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="1e083-168">A lógica é geralmente obtida com a propriedade `message_id` da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="1e083-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="1e083-169">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="1e083-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="1e083-170">Os tópicos e as assinaturas são persistentes e devem ser explicitamente excluídos por meio do [Portal do Azure][Azure portal] ou de forma programática.</span><span class="sxs-lookup"><span data-stu-id="1e083-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="1e083-171">O exemplo a seguir demonstra como excluir o tópico denominado `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="1e083-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="1e083-172">A exclusão de um tópico também exclui todas as assinaturas registradas com o tópico.</span><span class="sxs-lookup"><span data-stu-id="1e083-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="1e083-173">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="1e083-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="1e083-174">O código a seguir demonstra como excluir uma assinatura chamada `high-messages` do tópico `test-topic`:</span><span class="sxs-lookup"><span data-stu-id="1e083-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="1e083-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e083-175">Next steps</span></span>
<span data-ttu-id="1e083-176">Agora que você já sabe os princípios dos tópicos do Barramento de Serviço, acesse estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="1e083-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="1e083-177">Confira [Filas, tópicos e assinaturas](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="1e083-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="1e083-178">Referência da API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="1e083-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="1e083-179">Visite o repositório [SDK do Azure para o Ruby](https://github.com/Azure/azure-sdk-for-ruby) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e083-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
