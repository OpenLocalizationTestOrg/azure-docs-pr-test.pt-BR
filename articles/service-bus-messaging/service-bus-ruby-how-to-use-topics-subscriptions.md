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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="78164-104">Como toouse Service Bus tópicos e assinaturas com Ruby</span><span class="sxs-lookup"><span data-stu-id="78164-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="78164-105">Este artigo descreve como toouse Service Bus tópicos e assinaturas de aplicativos Ruby.</span><span class="sxs-lookup"><span data-stu-id="78164-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="78164-106">Olá cenários abordados incluem **criando tópicos e assinaturas, criando filtros de assinatura, enviando mensagens** tooa tópico **receber mensagens de uma assinatura**, e  **excluir tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="78164-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="78164-107">Para obter mais informações sobre os tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="78164-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="78164-108">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="78164-108">Create a topic</span></span>
<span data-ttu-id="78164-109">Olá **Azure::ServiceBusService** objeto permite que você toowork com tópicos.</span><span class="sxs-lookup"><span data-stu-id="78164-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="78164-110">Olá código a seguir cria um **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-111">toocreate um tópico, use Olá `create_topic()` método.</span><span class="sxs-lookup"><span data-stu-id="78164-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="78164-112">saudação de exemplo a seguir cria um tópico ou imprime erros Olá se houver.</span><span class="sxs-lookup"><span data-stu-id="78164-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="78164-113">Você também pode passar um **Azure::ServiceBus::Topic** objeto com opções adicionais, que permitem que você toooverride configurações do tópico como tamanho de fila toolive ou máximo de tempo de mensagem.</span><span class="sxs-lookup"><span data-stu-id="78164-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="78164-114">Olá exemplo a seguir mostra definindo o máximo da fila Olá too5 GB de tamanho e too1 toolive minutos de tempo:</span><span class="sxs-lookup"><span data-stu-id="78164-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="78164-115">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="78164-115">Create subscriptions</span></span>
<span data-ttu-id="78164-116">Assinaturas de tópico também são criadas com hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-117">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.</span><span class="sxs-lookup"><span data-stu-id="78164-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="78164-118">Assinaturas são persistentes e continuarão tooexist até a eles ou hello tópico eles estão associados são excluídos.</span><span class="sxs-lookup"><span data-stu-id="78164-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="78164-119">Se seu aplicativo contiver lógica toocreate uma assinatura, deve primeiro verificar se a assinatura de saudação já existe usando o método de getSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="78164-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="78164-120">Criar uma assinatura com o filtro saudação padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="78164-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="78164-121">Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada.</span><span class="sxs-lookup"><span data-stu-id="78164-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="78164-122">Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="78164-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="78164-123">Olá, exemplo a seguir cria uma assinatura chamada "todas as mensagens" e usa Olá padrão **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="78164-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="78164-124">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="78164-124">Create subscriptions with filters</span></span>
<span data-ttu-id="78164-125">Você também pode definir filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve ser exibidas dentro de uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="78164-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="78164-126">Olá, mais flexível tipo de filtro de assinaturas com suporte é Olá **Azure::ServiceBus::SqlFilter**, que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="78164-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="78164-127">Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="78164-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="78164-128">Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [SqlFilter](service-bus-messaging-sql-filter.md) sintaxe.</span><span class="sxs-lookup"><span data-stu-id="78164-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="78164-129">Você pode adicionar filtros tooa assinatura usando Olá `create_rule()` método hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-130">Esse método permite que você tooadd novos filtros tooan assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="78164-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="78164-131">Desde o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou Olá **MatchAll** substituirá os outros filtros que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="78164-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="78164-132">Você pode remover a regra padrão de saudação usando Olá `delete_rule()` método hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="78164-133">Olá, exemplo a seguir cria uma assinatura chamada "mensagens de alta" com um **Azure::ServiceBus::SqlFilter** que seleciona somente as mensagens que têm um personalizado `message_number` propriedade maior que 3:</span><span class="sxs-lookup"><span data-stu-id="78164-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="78164-134">Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `low-messages` com um **Azure::ServiceBus::SqlFilter** que seleciona somente as mensagens que têm um `message_number` propriedade menor ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="78164-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="78164-135">Quando uma mensagem agora é enviada muito`test-topic`, sempre será entregue tooreceivers inscrito toohello `all-messages` assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello `high-messages` e `low-messages` (de assinaturas de tópico Dependendo de conteúdo da mensagem de saudação).</span><span class="sxs-lookup"><span data-stu-id="78164-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="78164-136">Enviar tópico tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="78164-136">Send messages tooa topic</span></span>
<span data-ttu-id="78164-137">toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar Olá `send_topic_message()` método hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-138">As mensagens enviadas tooService tópicos do barramento são instâncias da saudação **Azure::ServiceBus::BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="78164-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="78164-139">**Azure::ServiceBus::BrokeredMessage** objetos têm um conjunto de propriedades padrão (como `label` e `time_to_live`), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="78164-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="78164-140">Um aplicativo pode definir o corpo de saudação da mensagem de saudação passando um toohello de valor de cadeia de caracteres `send_topic_message()` método e qualquer necessário propriedades padrão serão preenchidas por valores padrão.</span><span class="sxs-lookup"><span data-stu-id="78164-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="78164-141">Olá exemplo a seguir demonstra como teste toosend cinco mensagens muito`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="78164-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="78164-142">Observe que Olá `message_number` valor da propriedade personalizada de cada mensagem varia em iteração de saudação do loop de saudação (Isso determina qual assinatura recebe):</span><span class="sxs-lookup"><span data-stu-id="78164-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="78164-143">Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="78164-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="78164-144">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="78164-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="78164-145">Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico.</span><span class="sxs-lookup"><span data-stu-id="78164-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="78164-146">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="78164-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="78164-147">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="78164-147">Receive messages from a subscription</span></span>
<span data-ttu-id="78164-148">As mensagens são recebidas de uma assinatura usando Olá `receive_subscription_message()` método hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-149">Por padrão, as mensagens são read(peak) e bloqueado sem excluí-la da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="78164-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="78164-150">Você pode ler e excluir mensagem de saudação de assinatura Olá Olá configuração `peek_lock` opção muito**false**.</span><span class="sxs-lookup"><span data-stu-id="78164-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="78164-151">comportamento padrão de saudação torna Olá ler e excluir uma operação de duas etapas, que também torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="78164-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="78164-152">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78164-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="78164-153">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `delete_subscription_message()` método e fornecendo toobe de mensagem de saudação excluído como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="78164-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="78164-154">Olá `delete_subscription_message()` método será marcar a mensagem de saudação como sendo consumida e removê-lo da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="78164-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="78164-155">Se hello `:peek_lock` parâmetro está definido muito**false**, ler e excluir a mensagem de saudação torna-se o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processar uma mensagem no evento de saudação de um Falha.</span><span class="sxs-lookup"><span data-stu-id="78164-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="78164-156">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="78164-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="78164-157">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="78164-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="78164-158">Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="78164-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="78164-159">exemplo Hello primeiro recebe e exclui uma mensagem de saudação `low-messages` assinatura usando `:peek_lock` definido muito**false**, em seguida, ele recebe outra mensagem de saudação `high-messages` e, em seguida, exclui hello usando `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="78164-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="78164-160">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="78164-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="78164-161">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="78164-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="78164-162">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlock_subscription_message()` método hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="78164-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="78164-163">Isso faz com que saudação do barramento de serviço toounlock mensagem de assinatura do hello e torná-lo disponível toobe recebida novamente, ou por Olá mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="78164-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="78164-164">Também há um tempo limite associado a uma mensagem bloqueada em assinatura hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="78164-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="78164-165">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `delete_subscription_message()` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="78164-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="78164-166">Isso é geralmente chamado *, pelo menos, após processamento*; ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="78164-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="78164-167">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="78164-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="78164-168">Essa lógica geralmente é obtida usando Olá `message_id` propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="78164-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="78164-169">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="78164-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="78164-170">Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="78164-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="78164-171">exemplo Hello abaixo demonstra como o tópico de saudação toodelete nomeados `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="78164-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="78164-172">Excluir um tópico também exclui qualquer assinatura que é registrada com o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="78164-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="78164-173">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="78164-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="78164-174">Olá código a seguir demonstra como assinatura de saudação toodelete nomeados `high-messages` de saudação `test-topic` tópico:</span><span class="sxs-lookup"><span data-stu-id="78164-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="78164-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78164-175">Next steps</span></span>
<span data-ttu-id="78164-176">Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="78164-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="78164-177">Confira [Filas, tópicos e assinaturas](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="78164-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="78164-178">Referência da API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="78164-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="78164-179">Visite Olá [SDK do Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="78164-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
