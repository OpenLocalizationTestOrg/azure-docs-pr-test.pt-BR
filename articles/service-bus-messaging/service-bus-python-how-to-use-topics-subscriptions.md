---
title: "Como usar os tópicos do Barramento de Serviço do Azure com o Python | Microsoft Docs"
description: "Saiba como usar tópicos do Barramento de Serviço do Azure e assinaturas do Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 15269f9728e9dc45e6436e53b1859f76d4a7a0c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="72a5a-103">Como usar tópicos e assinaturas do Barramento de Serviço com Python</span><span class="sxs-lookup"><span data-stu-id="72a5a-103">How to use Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="72a5a-104">Este artigo descreve como usar tópicos e assinaturas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="72a5a-104">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="72a5a-105">Os exemplos são escritos em Python e usam o [pacote SDK para Azure Python][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="72a5a-105">The samples are written in Python and use the [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="72a5a-106">Os cenários abordados incluem a **criação de tópicos e assinaturas**, a **criação de filtros de assinatura**, o **envio de mensagens para um tópico**, o **recebimento de mensagens de uma assinatura** e a **exclusão de tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="72a5a-107">Para saber mais sobre tópicos e assinaturas, confira a seção [Próximas etapas](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="72a5a-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="72a5a-108">Se você precisar instalar o Python ou o [pacote do Azure Python][Azure Python package], confira o [Guia de instalação do Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="72a5a-108">If you need to install Python or the [Azure Python package][Azure Python package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="72a5a-109">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="72a5a-109">Create a topic</span></span>
<span data-ttu-id="72a5a-110">O objeto **ServiceBusService** permite que você trabalhe com tópicos.</span><span class="sxs-lookup"><span data-stu-id="72a5a-110">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="72a5a-111">Adicione o seguinte próximo à parte superior de qualquer arquivo do Python no qual você deseja acessar o Barramento de Serviço de forma programática:</span><span class="sxs-lookup"><span data-stu-id="72a5a-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="72a5a-112">O código a seguir cria um objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-112">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="72a5a-113">Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace real e pelo nome e valor da chave de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="72a5a-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="72a5a-114">Você pode obter os valores de nome e valor da chave da SAS no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="72a5a-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="72a5a-115">O método `create_topic` também dá suporte a opções adicionais, que permitem substituir configurações padrão do tópico, como a vida útil da mensagem ou o tamanho máximo do tópico.</span><span class="sxs-lookup"><span data-stu-id="72a5a-115">The `create_topic` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="72a5a-116">O seguinte exemplo define o tamanho máximo do tópico como 5 GB e o valor de TTL (vida útil) como um minuto:</span><span class="sxs-lookup"><span data-stu-id="72a5a-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="72a5a-117">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="72a5a-117">Create subscriptions</span></span>
<span data-ttu-id="72a5a-118">As assinaturas de tópicos também são criadas com o objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="72a5a-119">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de mensagens entregues à fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="72a5a-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="72a5a-120">As assinaturas são persistentes e continuarão existindo até que elas ou o tópico ao qual estão inscritas sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="72a5a-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="72a5a-121">Criar uma assinatura com o filtro padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="72a5a-121">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="72a5a-122">O filtro **MatchAll** será o padrão usado se nenhum filtro for especificado quando uma nova assinatura for criada.</span><span class="sxs-lookup"><span data-stu-id="72a5a-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="72a5a-123">Quando o filtro **MatchAll** é usado, todas as mensagens publicadas no tópico são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="72a5a-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="72a5a-124">O exemplo a seguir cria uma assinatura denominada `AllMessages` e usa o filtro padrão **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-124">The following example creates a subscription named `AllMessages` and uses the default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="72a5a-125">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="72a5a-125">Create subscriptions with filters</span></span>
<span data-ttu-id="72a5a-126">Você também pode definir filtros que permitem especificar quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica do tópico.</span><span class="sxs-lookup"><span data-stu-id="72a5a-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="72a5a-127">O tipo de filtro mais flexível compatível com as assinaturas é um **SqlFilter**, que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="72a5a-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="72a5a-128">Os filtros SQL operam nas propriedades das mensagens que são publicadas no tópico.</span><span class="sxs-lookup"><span data-stu-id="72a5a-128">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="72a5a-129">Para saber mais sobre as expressões que podem ser usadas com um filtro SQL, confira a sintaxe [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="72a5a-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="72a5a-130">É possível adicionar filtros a uma assinatura usando o método **create\_rule** do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="72a5a-131">Este método permite que você adicione novos filtros a uma assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="72a5a-131">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="72a5a-132">Como o filtro padrão é aplicado automaticamente em todas as assinaturas novas, você deve primeiro remover o filtro padrão, senão o filtro **MatchAll** substituirá todos os outros filtros que você possa especificar.</span><span class="sxs-lookup"><span data-stu-id="72a5a-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="72a5a-133">Você pode remover a regra padrão usando o método `delete_rule` do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-133">You can remove the default rule by using the `delete_rule` method of the **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="72a5a-134">O exemplo a seguir cria uma assinatura denominada `HighMessages` com um **SqlFilter** que seleciona apenas as mensagens que tenham uma propriedade personalizada `messagenumber` maior que 3:</span><span class="sxs-lookup"><span data-stu-id="72a5a-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="72a5a-135">Da mesma forma, o seguinte exemplo cria uma assinatura denominada `LowMessages` com um **SqlFilter** que seleciona apenas mensagens que têm uma propriedade `messagenumber` menor ou igual a 3:</span><span class="sxs-lookup"><span data-stu-id="72a5a-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="72a5a-136">Agora, quando uma mensagem for enviada para `mytopic`, ela sempre será fornecida aos destinatários inscritos na assinatura do tópico **AllMessages** e será fornecida de forma seletiva para os destinatários inscritos nas assinaturas dos tópicos **HighMessages** e **LowMessages** (dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="72a5a-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="72a5a-137">Enviar mensagens para um tópico</span><span class="sxs-lookup"><span data-stu-id="72a5a-137">Send messages to a topic</span></span>
<span data-ttu-id="72a5a-138">Para enviar uma mensagem a um tópico do Barramento de Serviço, seu aplicativo deve usar o método `send_topic_message` do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-138">To send a message to a Service Bus topic, your application must use the `send_topic_message` method of the **ServiceBusService** object.</span></span>

<span data-ttu-id="72a5a-139">O exemplo a seguir demonstra como enviar cinco mensagens de teste para `mytopic`.</span><span class="sxs-lookup"><span data-stu-id="72a5a-139">The following example demonstrates how to send five test messages to `mytopic`.</span></span> <span data-ttu-id="72a5a-140">Observe que o valor da propriedade `messagenumber` de cada mensagem varia de acordo com a iteração do loop (isso determina quais assinaturas a receberão):</span><span class="sxs-lookup"><span data-stu-id="72a5a-140">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="72a5a-141">Os tópicos do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="72a5a-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="72a5a-142">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="72a5a-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="72a5a-143">Não há nenhum limite no número de mensagens mantidas em um tópico, mas há uma capacidade do tamanho total das mensagens mantidas por um tópico.</span><span class="sxs-lookup"><span data-stu-id="72a5a-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="72a5a-144">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="72a5a-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="72a5a-145">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="72a5a-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="72a5a-146">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="72a5a-146">Receive messages from a subscription</span></span>
<span data-ttu-id="72a5a-147">As mensagens são recebidas de uma assinatura usando o método `receive_subscription_message` no objeto **ServiceBusService**:</span><span class="sxs-lookup"><span data-stu-id="72a5a-147">Messages are received from a subscription using the `receive_subscription_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="72a5a-148">As mensagens são excluídas da assinatura conforme são lidas quando o parâmetro `peek_lock` é definido como **False**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-148">Messages are deleted from the subscription as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="72a5a-149">Você pode ler (espiar) e bloquear a mensagem sem excluí-la da fila ao definir o parâmetro `peek_lock` como **True**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="72a5a-150">O comportamento da leitura e da exclusão da mensagem como parte da operação de recebimento é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo possa tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="72a5a-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="72a5a-151">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="72a5a-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="72a5a-152">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="72a5a-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="72a5a-153">Se o parâmetro `peek_lock` estiver definido como **True**, o processo de recebimento se torna uma operação de duas etapas, o que torna possível o suporte a aplicativos que não toleram mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="72a5a-153">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="72a5a-154">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72a5a-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="72a5a-155">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para o processamento futuro), ele conclui a segunda etapa do processo de recebimento chamando o método `delete` no objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete` method on the **Message** object.</span></span> <span data-ttu-id="72a5a-156">O método `delete` marcará a mensagem como sendo consumida e a removerá da assinatura.</span><span class="sxs-lookup"><span data-stu-id="72a5a-156">The `delete` method marks the message as being consumed and removes it from the subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="72a5a-157">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="72a5a-157">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="72a5a-158">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="72a5a-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="72a5a-159">Se um aplicativo receptor não conseguir processar a mensagem por algum motivo, ele chamará o método `unlock` no objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="72a5a-159">If a receiver application is unable to process the message for some reason, then it can call the `unlock` method on the **Message** object.</span></span> <span data-ttu-id="72a5a-160">Isso fará com que o Barramento de Serviço desbloqueie a mensagem na assinatura e disponibilize-a para ser recebida novamente, pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="72a5a-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="72a5a-161">Também há um tempo limite associado a uma mensagem bloqueada na assinatura e, se houver falha no processamento da mensagem pelo aplicativo antes da expiração do tempo limite de bloqueio (por exemplo, se o aplicativo travar), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="72a5a-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="72a5a-162">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método `delete` seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="72a5a-162">In the event that the application crashes after processing the message but before the `delete` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="72a5a-163">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="72a5a-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="72a5a-164">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="72a5a-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="72a5a-165">Isso geralmente é obtido com a propriedade **MessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="72a5a-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="72a5a-166">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="72a5a-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="72a5a-167">Os tópicos e as assinaturas são persistentes e devem ser explicitamente excluídos por meio do [Portal do Azure][Azure portal] ou de forma programática.</span><span class="sxs-lookup"><span data-stu-id="72a5a-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="72a5a-168">O seguinte exemplo mostra como excluir o tópico chamado `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="72a5a-168">The following example shows how to delete the topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="72a5a-169">A exclusão de um tópico também exclui todas as assinaturas registradas com o tópico.</span><span class="sxs-lookup"><span data-stu-id="72a5a-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="72a5a-170">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="72a5a-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="72a5a-171">O seguinte código mostra como excluir uma assinatura chamada `HighMessages` do tópico `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="72a5a-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="72a5a-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72a5a-172">Next steps</span></span>
<span data-ttu-id="72a5a-173">Agora que você já sabe os princípios dos tópicos do Barramento de Serviço, acesse estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="72a5a-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="72a5a-174">Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="72a5a-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="72a5a-175">Referência para [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="72a5a-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
