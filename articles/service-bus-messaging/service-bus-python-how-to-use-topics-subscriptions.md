---
title: "tópicos de barramento de serviço do Azure toouse aaaHow com Python | Microsoft Docs"
description: "Saiba como toouse Azure Service Bus tópicos e assinaturas do Python."
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
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="500c4-103">Como toouse Service Bus tópicos e assinaturas com Python</span><span class="sxs-lookup"><span data-stu-id="500c4-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="500c4-104">Este artigo descreve como toouse Service Bus tópicos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="500c4-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="500c4-105">exemplos de saudação são escritos em Python e usar Olá [pacote do Azure SDK de Python][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="500c4-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="500c4-106">Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="500c4-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="500c4-107">Para obter mais informações sobre tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="500c4-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="500c4-108">Se você precisar tooinstall Python ou Olá [pacote do Azure Python][Azure Python package], consulte Olá [guia de instalação do Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="500c4-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="500c4-109">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="500c4-109">Create a topic</span></span>
<span data-ttu-id="500c4-110">Olá **ServiceBusService** objeto permite que você toowork com tópicos.</span><span class="sxs-lookup"><span data-stu-id="500c4-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="500c4-111">Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="500c4-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="500c4-112">Olá código a seguir cria um **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="500c4-113">Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace real e pelo nome e valor da chave de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="500c4-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="500c4-114">Você pode obter valores de saudação para o nome da chave SAS hello e valor de Olá [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="500c4-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="500c4-115">Olá `create_topic` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações do tópico como tamanho de tópico toolive ou máximo de tempo de mensagem.</span><span class="sxs-lookup"><span data-stu-id="500c4-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="500c4-116">Olá exemplo a seguir define Olá máximo do tópico tamanho too5 GB e um valor de (vida útil TTL) toolive tempo de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="500c4-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="500c4-117">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="500c4-117">Create subscriptions</span></span>
<span data-ttu-id="500c4-118">Assinaturas tootopics também são criados com hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="500c4-119">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.</span><span class="sxs-lookup"><span data-stu-id="500c4-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="500c4-120">Assinaturas são persistentes e continuarão tooexist até a eles ou hello toowhich tópico se inscreveu, serão excluídas.</span><span class="sxs-lookup"><span data-stu-id="500c4-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="500c4-121">Criar uma assinatura com o filtro saudação padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="500c4-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="500c4-122">Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada.</span><span class="sxs-lookup"><span data-stu-id="500c4-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="500c4-123">Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="500c4-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="500c4-124">Olá, exemplo a seguir cria uma assinatura chamada `AllMessages` e usa Olá padrão **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="500c4-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="500c4-125">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="500c4-125">Create subscriptions with filters</span></span>
<span data-ttu-id="500c4-126">Você também pode definir filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.</span><span class="sxs-lookup"><span data-stu-id="500c4-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="500c4-127">Hello mais flexível o tipo de filtro de assinaturas com suporte é um **SqlFilter**, que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="500c4-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="500c4-128">Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="500c4-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="500c4-129">Para obter mais informações sobre expressões de saudação que pode ser usado com um filtro SQL, consulte Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.</span><span class="sxs-lookup"><span data-stu-id="500c4-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="500c4-130">Você pode adicionar filtros tooa assinatura usando Olá **criar\_regra** método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="500c4-131">Esse método permite que você tooadd novos filtros tooan assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="500c4-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="500c4-132">Porque o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou hello **MatchAll** substituirá os outros filtros que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="500c4-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="500c4-133">Você pode remover a regra padrão de saudação usando Olá `delete_rule` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="500c4-134">Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `messagenumber` propriedade maior que 3:</span><span class="sxs-lookup"><span data-stu-id="500c4-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="500c4-135">Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um `messagenumber` propriedade menor ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="500c4-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="500c4-136">Agora, quando uma mensagem é enviada muito`mytopic` toohello tooreceivers inscrito sempre é fornecida **AllMessages** assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello **HighMessages**  e **LowMessages** assinaturas de tópico (dependendo do conteúdo da mensagem de saudação).</span><span class="sxs-lookup"><span data-stu-id="500c4-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="500c4-137">Enviar tópico tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="500c4-137">Send messages tooa topic</span></span>
<span data-ttu-id="500c4-138">toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar Olá `send_topic_message` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="500c4-139">Olá exemplo a seguir demonstra como teste toosend cinco mensagens muito`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="500c4-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="500c4-140">Observe que Olá `messagenumber` varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (Isso determina quais assinaturas recebem-lo):</span><span class="sxs-lookup"><span data-stu-id="500c4-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="500c4-141">Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="500c4-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="500c4-142">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="500c4-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="500c4-143">Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico.</span><span class="sxs-lookup"><span data-stu-id="500c4-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="500c4-144">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="500c4-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="500c4-145">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="500c4-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="500c4-146">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="500c4-146">Receive messages from a subscription</span></span>
<span data-ttu-id="500c4-147">As mensagens são recebidas de uma assinatura usando Olá `receive_subscription_message` método hello **ServiceBusService** objeto:</span><span class="sxs-lookup"><span data-stu-id="500c4-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="500c4-148">As mensagens serão excluídas da assinatura Olá conforme elas são de leitura quando Olá parâmetro `peek_lock` está definido muito**False**.</span><span class="sxs-lookup"><span data-stu-id="500c4-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="500c4-149">Você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro de saudação configuração `peek_lock` muito**True**.</span><span class="sxs-lookup"><span data-stu-id="500c4-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="500c4-150">Olá comportamento de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="500c4-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="500c4-151">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="500c4-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="500c4-152">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="500c4-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="500c4-153">Se hello `peek_lock` parâmetro está definido muito**True**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="500c4-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="500c4-154">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="500c4-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="500c4-155">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `delete` método hello **mensagem** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="500c4-156">Olá `delete` método marca a mensagem de saudação como sendo consumida e remove da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="500c4-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="500c4-157">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="500c4-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="500c4-158">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="500c4-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="500c4-159">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlock` método hello **mensagem** objeto.</span><span class="sxs-lookup"><span data-stu-id="500c4-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="500c4-160">Isso causar a mensagem de saudação do barramento de serviço toounlock de assinatura do hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="500c4-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="500c4-161">Também há um tempo limite associado a uma mensagem bloqueada em assinatura hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e a mensagem de saudação desbloqueia o barramento de serviço automaticamente e o torna disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="500c4-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="500c4-162">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `delete` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="500c4-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="500c4-163">Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="500c4-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="500c4-164">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="500c4-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="500c4-165">Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="500c4-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="500c4-166">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="500c4-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="500c4-167">Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="500c4-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="500c4-168">Olá exemplo a seguir mostra como o tópico de saudação toodelete chamado `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="500c4-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="500c4-169">Excluir um tópico também exclui qualquer assinatura que é registrada com o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="500c4-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="500c4-170">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="500c4-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="500c4-171">Olá código a seguir mostra como toodelete uma assinatura chamada `HighMessages` de saudação `mytopic` tópico:</span><span class="sxs-lookup"><span data-stu-id="500c4-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="500c4-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="500c4-172">Next steps</span></span>
<span data-ttu-id="500c4-173">Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="500c4-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="500c4-174">Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="500c4-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="500c4-175">Referência para [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="500c4-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
