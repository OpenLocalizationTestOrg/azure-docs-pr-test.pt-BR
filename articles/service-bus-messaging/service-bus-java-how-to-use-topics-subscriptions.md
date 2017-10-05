---
title: "Como usar os tópicos de Barramento de Serviço do Azure com Java | Microsoft Docs"
description: "Use tópicos e assinaturas do Barramento de Serviço no Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="1ad05-103">Como usar tópicos e assinaturas do Barramento de Serviço com Java</span><span class="sxs-lookup"><span data-stu-id="1ad05-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="1ad05-104">Este guia descreve como usar assinaturas e tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="1ad05-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="1ad05-105">As amostras são gravadas em Java e usam o [SDK do Azure para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="1ad05-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="1ad05-106">Os cenários abordados incluem a **criação de tópicos e assinaturas**, a **criação de filtros de assinatura**, o **envio de mensagens para um tópico**, o **recebimento de mensagens de uma assinatura** e a **exclusão de tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="1ad05-107">O que são os tópicos e as assinaturas do Barramento de Serviço?</span><span class="sxs-lookup"><span data-stu-id="1ad05-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="1ad05-108">Os tópicos e assinaturas do Barramento de Serviço dão suporte a um modelo de comunicação de mensagens de *publicação/assinatura* .</span><span class="sxs-lookup"><span data-stu-id="1ad05-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="1ad05-109">Durante o uso de tópicos e assinaturas, os componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, eles trocam mensagens por meio de um tópico, que atua como um intermediário.</span><span class="sxs-lookup"><span data-stu-id="1ad05-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![Conceitos de tópico](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="1ad05-111">Em contraste com as filas do Barramento de Serviço, em que cada mensagem é processada por um único consumidor, tópicos e assinaturas fornecem uma forma de comunicação de um para muitos usando um padrão de publicação/assinatura.</span><span class="sxs-lookup"><span data-stu-id="1ad05-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="1ad05-112">É possível registrar várias assinaturas para um tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="1ad05-113">Quando uma mensagem é enviada a um tópico, é disponibilizada para cada assinatura para ser manipulada/processada de forma independente.</span><span class="sxs-lookup"><span data-stu-id="1ad05-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="1ad05-114">Uma assinatura de tópico é semelhante a uma fila virtual que recebe cópias das mensagens enviadas para o tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="1ad05-115">Outra opção é registrar regras de filtro para um tópico por assinatura, o que permite que você filtre/restrinja quais mensagens para um tópico são recebidas por quais assinaturas de tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="1ad05-116">As assinaturas e os tópicos do Barramento de Serviço permitem o dimensionamento para processar um grande número de mensagens em muitos usuários e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1ad05-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="1ad05-117">Criar um namespace de serviço</span><span class="sxs-lookup"><span data-stu-id="1ad05-117">Create a service namespace</span></span>
<span data-ttu-id="1ad05-118">Para começar a usar tópicos e assinaturas do Barramento de Serviço no Azure, primeiramente, é preciso criar um namespace, que fornece um contêiner de controle para lidar com recursos do Barramento de Serviço no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad05-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="1ad05-119">Para criar um namespace:</span><span class="sxs-lookup"><span data-stu-id="1ad05-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="1ad05-120">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="1ad05-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="1ad05-121">Verifique se você instalou o [SDK do Azure para Java][Azure SDK for Java] antes de compilar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="1ad05-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="1ad05-122">Se estiver usando o Eclipse, instale o [Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse], que inclui o SDK do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="1ad05-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="1ad05-123">Você pode adicionar as **Bibliotecas do Microsoft Azure para Java** ao seu projeto:</span><span class="sxs-lookup"><span data-stu-id="1ad05-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="1ad05-124">Adicione as seguintes instruções `import` à parte superior do arquivo Java:</span><span class="sxs-lookup"><span data-stu-id="1ad05-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="1ad05-125">Adicione as Bibliotecas do Azure para Java a seu caminho de compilação e inclua-o em seu assembly de implantação do projeto.</span><span class="sxs-lookup"><span data-stu-id="1ad05-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="1ad05-126">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="1ad05-126">Create a topic</span></span>
<span data-ttu-id="1ad05-127">As operações de gerenciamento dos tópicos do Barramento de Serviço podem ser executadas pela classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="1ad05-128">Um objeto **ServiceBusContract** é construído com uma configuração adequada que encapsula o token SAS com as permissões para gerenciá-lo, e a classe **ServiceBusContract** é o único ponto de comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad05-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="1ad05-129">A classe **ServiceBusService** oferece métodos para criar, enumerar e excluir tópicos.</span><span class="sxs-lookup"><span data-stu-id="1ad05-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="1ad05-130">O exemplo abaixo mostra como um objeto **ServiceBusService** pode ser usado para criar um tópico chamado `TestTopic` com um namespace chamado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="1ad05-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="1ad05-131">Existem métodos em **TopicInfo** que permitem a definição das propriedades do tópico (por exemplo: para definir o valor padrão da TTL [vida útil] a ser aplicado às mensagens enviadas para o tópico).</span><span class="sxs-lookup"><span data-stu-id="1ad05-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="1ad05-132">O exemplo a seguir mostra como criar um tópico denominado `TestTopic` com um tamanho máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="1ad05-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="1ad05-133">Observe que você pode usar o método **listTopics** nos objetos **ServiceBusContract** para verificar se um tópico com um nome especificado já existe dentro de um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="1ad05-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="1ad05-134">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="1ad05-134">Create subscriptions</span></span>
<span data-ttu-id="1ad05-135">As assinaturas de tópicos também são criadas com a classe **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="1ad05-136">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de mensagens passadas para a fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1ad05-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="1ad05-137">Criar uma assinatura com o filtro padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="1ad05-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="1ad05-138">O filtro **MatchAll** será o padrão usado se nenhum filtro for especificado quando uma nova assinatura for criada.</span><span class="sxs-lookup"><span data-stu-id="1ad05-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="1ad05-139">Quando o filtro **MatchAll** é usado, todas as mensagens publicadas no tópico são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1ad05-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="1ad05-140">O exemplo a seguir cria uma assinatura denominada “AllMessages” e usa o filtro padrão **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="1ad05-141">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="1ad05-141">Create subscriptions with filters</span></span>
<span data-ttu-id="1ad05-142">Você também pode configurar filtros que permitem definir um escopo de quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica do tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="1ad05-143">O tipo de filtro mais flexível com suporte com as assinaturas é o [SqlFilter][SqlFilter], que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="1ad05-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="1ad05-144">Os filtros SQL operam nas propriedades das mensagens que são publicadas no tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="1ad05-145">Para obter mais detalhes sobre as expressões que podem ser usadas com um filtro SQL, examine a sintaxe [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="1ad05-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="1ad05-146">O exemplo a seguir cria uma assinatura denominada `HighMessages` com um objeto [SqlFilter][SqlFilter] que seleciona apenas as mensagens que têm uma propriedade **MessageNumber** personalizada maior do que 3:</span><span class="sxs-lookup"><span data-stu-id="1ad05-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="1ad05-147">De maneira semelhante, o exemplo a seguir cria uma assinatura denominada `LowMessages` com um objeto [SqlFilter][SqlFilter] que seleciona apenas as mensagens que têm uma propriedade **MessageNumber** menor ou igual a 3:</span><span class="sxs-lookup"><span data-stu-id="1ad05-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="1ad05-148">Quando uma mensagem é agora enviada para `TestTopic`, ela sempre será entregue aos destinatários inscritos na assinatura de `AllMessages` e entregue de forma seletiva aos destinatários inscritos nas assinaturas de `HighMessages` e `LowMessages` (dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="1ad05-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="1ad05-149">Enviar mensagens para um tópico</span><span class="sxs-lookup"><span data-stu-id="1ad05-149">Send messages to a topic</span></span>
<span data-ttu-id="1ad05-150">Para enviar uma mensagem a um tópico do Barramento de Serviço, seu aplicativo obtém um objeto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="1ad05-151">O código abaixo demonstra como enviar uma mensagem ao tópico `TestTopic` criado anteriormente no namespace `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="1ad05-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="1ad05-152">As mensagens enviadas aos Tópicos de Barramento de Serviço são instâncias da classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="1ad05-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="1ad05-153">Os objetos [BrokeredMessage][BrokeredMessage]* têm um conjunto de métodos padrão (como **setLabel** e **TimeToLive**), um dicionário usado para armazenar propriedades personalizadas específicas ao aplicativo e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad05-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="1ad05-154">Um aplicativo pode definir o corpo da mensagem passando um objeto serializável para o construtor da [BrokeredMessage][BrokeredMessage] e o **DataContractSerializer** adequado será então usado para serializar o objeto.</span><span class="sxs-lookup"><span data-stu-id="1ad05-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="1ad05-155">Como alternativa, um **java.io.InputStream** pode ser fornecido.</span><span class="sxs-lookup"><span data-stu-id="1ad05-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="1ad05-156">O exemplo a seguir demonstra como enviar cinco mensagens de teste para `TestTopic` **MessageSender** que obtivemos no trecho de código acima.</span><span class="sxs-lookup"><span data-stu-id="1ad05-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="1ad05-157">Observe como o valor da propriedade **MessageNumber** de cada mensagem varia de acordo com a iteração do loop (isso determinará quais assinaturas o receberá):</span><span class="sxs-lookup"><span data-stu-id="1ad05-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="1ad05-158">Os tópicos do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1ad05-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1ad05-159">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1ad05-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1ad05-160">Não há nenhum limite no número de mensagens mantidas em um tópico, mas há um limite no tamanho total das mensagens mantidas por um tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="1ad05-161">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1ad05-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="1ad05-162">Como receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="1ad05-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="1ad05-163">Para receber mensagens de uma assinatura, use um objeto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="1ad05-164">As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="1ad05-165">Ao usar o modo **ReceiveAndDelete**, o recebimento é uma operação única, isto é, quando o Barramento de Serviço recebe uma solicitação de leitura de uma mensagem, ele marca a mensagem como sendo consumida e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad05-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="1ad05-166">O modo **ReceiveAndDelete** é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo pode tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="1ad05-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1ad05-167">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="1ad05-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1ad05-168">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="1ad05-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1ad05-169">No modo **PeekLock**, o recebimento de uma mensagem se torna uma operação de dois estágios, o que possibilita o suporte aos aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="1ad05-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1ad05-170">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad05-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1ad05-171">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para processamento futuro), ele conclui a segunda etapa do processo de recebimento chamando **Delete** na mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="1ad05-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="1ad05-172">Quando o Barramento de Serviço vê a chamada **Delete**, ele marca a mensagem como sendo consumida e a remove do tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="1ad05-173">O exemplo abaixo demonstra como as mensagens podem ser recebidas e processadas usando o modo **PeekLock** (não o modo padrão).</span><span class="sxs-lookup"><span data-stu-id="1ad05-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="1ad05-174">O exemplo a seguir executa um loop e processa mensagens na assinatura "HighMessages" e, em seguida, sai quando não há mais mensagens (como alternativa, pode ser configurado para aguardar novas mensagens).</span><span class="sxs-lookup"><span data-stu-id="1ad05-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1ad05-175">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="1ad05-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="1ad05-176">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="1ad05-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1ad05-177">Se um aplicativo receptor não for capaz de processar a mensagem por algum motivo, ele chamará o método **unlockMessage** na mensagem recebida (em vez do método **deleteMessage**).</span><span class="sxs-lookup"><span data-stu-id="1ad05-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="1ad05-178">Isso fará com que o Barramento de Serviço desbloqueie a mensagem no tópico e a disponibilize para que seja recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="1ad05-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1ad05-179">Também há um tempo limite associado a uma mensagem bloqueada no tópico e, se o aplicativo não conseguir processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, em caso de falha do aplicativo), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="1ad05-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="1ad05-180">Se houver falha do aplicativo após o processamento da mensagem, mas antes da solicitação **deleteMessage** ser emitida, a mensagem será entregue novamente ao aplicativo quando ele reiniciar.</span><span class="sxs-lookup"><span data-stu-id="1ad05-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="1ad05-181">Isso é frequentemente chamado de **Processamento de pelo menos uma vez**, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="1ad05-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1ad05-182">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="1ad05-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="1ad05-183">Isso geralmente é feito com o método **getMessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="1ad05-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="1ad05-184">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="1ad05-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="1ad05-185">A principal maneira de excluir tópicos e assinaturas é usar um objeto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="1ad05-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="1ad05-186">A exclusão de um tópico também excluirá todas as assinaturas registradas com o tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad05-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="1ad05-187">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="1ad05-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="1ad05-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ad05-188">Next Steps</span></span>
<span data-ttu-id="1ad05-189">Agora que você aprendeu as noções básicas sobre as filas do Barramento de Serviço, veja [Filas, tópicos e assinaturas do Barramento de Serviço][Service Bus queues, topics, and subscriptions] para saber mais.</span><span class="sxs-lookup"><span data-stu-id="1ad05-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
