---
title: "tópicos de barramento de serviço do Azure toouse aaaHow com Java | Microsoft Docs"
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
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="71d36-103">Como toouse Service Bus tópicos e assinaturas com Java</span><span class="sxs-lookup"><span data-stu-id="71d36-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="71d36-104">Este guia descreve como toouse Service Bus tópicos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="71d36-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="71d36-105">exemplos de saudação são escritos em Java e usam Olá [SDK do Azure para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="71d36-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="71d36-106">Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="71d36-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="71d36-107">O que são os tópicos e as assinaturas do Barramento de Serviço?</span><span class="sxs-lookup"><span data-stu-id="71d36-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="71d36-108">Os tópicos e assinaturas do Barramento de Serviço dão suporte a um modelo de comunicação de mensagens de *publicação/assinatura* .</span><span class="sxs-lookup"><span data-stu-id="71d36-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="71d36-109">Durante o uso de tópicos e assinaturas, os componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, eles trocam mensagens por meio de um tópico, que atua como um intermediário.</span><span class="sxs-lookup"><span data-stu-id="71d36-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![Conceitos de tópico](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="71d36-111">Em contraste com as filas do Barramento de Serviço, em que cada mensagem é processada por um único consumidor, tópicos e assinaturas fornecem uma forma de comunicação de um para muitos usando um padrão de publicação/assinatura.</span><span class="sxs-lookup"><span data-stu-id="71d36-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="71d36-112">É possível registrar o tópico de tooa várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="71d36-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="71d36-113">Quando uma mensagem é enviada tooa tópico, ele é feito tooeach disponível assinatura toohandle/processo independentemente.</span><span class="sxs-lookup"><span data-stu-id="71d36-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="71d36-114">Um tópico de tooa de assinatura é semelhante a uma fila virtual que recebe cópias das mensagens de saudação enviadas toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="71d36-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="71d36-115">Opcionalmente, você pode registrar as regras de filtro para um tópico em uma base por assinatura, que permite que você toofilter/restringir o tópico de tooa quais mensagens são recebidas por quais assinaturas de tópico.</span><span class="sxs-lookup"><span data-stu-id="71d36-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="71d36-116">Assinaturas e tópicos do barramento de serviço permitem tooscale tooprocess um grande número de mensagens em um número muito grande de usuários e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="71d36-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="71d36-117">Criar um namespace de serviço</span><span class="sxs-lookup"><span data-stu-id="71d36-117">Create a service namespace</span></span>
<span data-ttu-id="71d36-118">toobegin usando assinaturas e tópicos do barramento de serviço no Azure, você deve primeiro criar um namespace, que fornece um contêiner de escopo para endereçar recursos de barramento de serviço dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71d36-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="71d36-119">toocreate um namespace:</span><span class="sxs-lookup"><span data-stu-id="71d36-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="71d36-120">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="71d36-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="71d36-121">Verifique se você instalou Olá [SDK do Azure para Java] [ Azure SDK for Java] antes de compilar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="71d36-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="71d36-122">Se você estiver usando o Eclipse, você pode instalar Olá [Kit de ferramentas do Azure para Eclipse] [ Azure Toolkit for Eclipse] que inclui Olá SDK do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="71d36-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="71d36-123">Você pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:</span><span class="sxs-lookup"><span data-stu-id="71d36-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="71d36-124">Adicione o seguinte Olá `import` superior de toohello instruções saudação do arquivo de Java:</span><span class="sxs-lookup"><span data-stu-id="71d36-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="71d36-125">Adicione Olá bibliotecas do Azure para Java tooyour caminho de compilação e incluí-lo em seu assembly de implantação do projeto.</span><span class="sxs-lookup"><span data-stu-id="71d36-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="71d36-126">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="71d36-126">Create a topic</span></span>
<span data-ttu-id="71d36-127">As operações de gerenciamento dos tópicos do Barramento de Serviço podem ser executadas pela classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="71d36-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="71d36-128">Um **ServiceBusContract** objeto for construído com uma configuração apropriada que encapsula o token SAS com toomanage de permissões e hello **ServiceBusContract** classe é um ponto único de saudação de comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="71d36-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="71d36-129">Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e excluir tópicos.</span><span class="sxs-lookup"><span data-stu-id="71d36-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="71d36-130">Olá mostrado no exemplo a seguir como um **ServiceBusService** objeto pode ser usado toocreate um tópico chamado `TestTopic`, com um namespace chamado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="71d36-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="71d36-131">Há métodos em **TopicInfo** que permitem a propriedades de tópico Olá a ser definido (por exemplo: tooset saudação padrão time-to-live (TTL) valor toobe aplicada toomessages enviados toohello tópico).</span><span class="sxs-lookup"><span data-stu-id="71d36-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="71d36-132">Olá exemplo a seguir mostra como toocreate um tópico chamado `TestTopic` com um tamanho máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="71d36-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="71d36-133">Observe que você pode usar o hello **listTopics** método **ServiceBusContract** objetos toocheck se um tópico com um nome especificado já existe em um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="71d36-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="71d36-134">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="71d36-134">Create subscriptions</span></span>
<span data-ttu-id="71d36-135">Assinaturas tootopics também são criados com hello **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="71d36-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="71d36-136">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens passado a fila virtual toohello da assinatura.</span><span class="sxs-lookup"><span data-stu-id="71d36-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="71d36-137">Criar uma assinatura com o filtro saudação padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="71d36-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="71d36-138">Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada.</span><span class="sxs-lookup"><span data-stu-id="71d36-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="71d36-139">Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="71d36-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="71d36-140">Olá, exemplo a seguir cria uma assinatura chamada "AllMessages" e usa Olá padrão **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="71d36-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="71d36-141">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="71d36-141">Create subscriptions with filters</span></span>
<span data-ttu-id="71d36-142">Você também pode criar filtros que permitem que você tooscope quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.</span><span class="sxs-lookup"><span data-stu-id="71d36-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="71d36-143">Hello mais flexível o tipo de filtro de assinaturas com suporte é o [SqlFilter][SqlFilter], que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="71d36-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="71d36-144">Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="71d36-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="71d36-145">Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.</span><span class="sxs-lookup"><span data-stu-id="71d36-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="71d36-146">Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um [SqlFilter] [ SqlFilter] objeto que seleciona somente as mensagens que têm um personalizado **MessageNumber** propriedade maior que 3:</span><span class="sxs-lookup"><span data-stu-id="71d36-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="71d36-147">Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um [SqlFilter] [ SqlFilter] objeto que seleciona somente as mensagens que têm um **MessageNumber** propriedade menor ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="71d36-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="71d36-148">Quando uma mensagem agora é enviada muito`TestTopic`, ela será sempre entregue tooreceivers inscrito toohello `AllMessages` assinatura e toohello tooreceivers seletivamente entregue inscrito `HighMessages` e `LowMessages` (assinaturas Dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="71d36-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="71d36-149">Enviar tópico tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="71d36-149">Send messages tooa topic</span></span>
<span data-ttu-id="71d36-150">toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo obtém um **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="71d36-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="71d36-151">Olá código a seguir demonstra como uma mensagem de saudação do toosend `TestTopic` tópico criado anteriormente no hello `HowToSample` namespace:</span><span class="sxs-lookup"><span data-stu-id="71d36-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="71d36-152">As mensagens enviadas tooService tópicos do barramento são instâncias da [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="71d36-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="71d36-153">[BrokeredMessage][BrokeredMessage]* objetos têm um conjunto de métodos padrão (como **setLabel** e **TimeToLive**), um dicionário que é usado toohold personalizado propriedades específicas do aplicativo e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71d36-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="71d36-154">Um aplicativo pode definir o corpo de saudação da mensagem passando qualquer objeto serializável para construtor de saudação do [BrokeredMessage][BrokeredMessage]e hello apropriado **DataContractSerializer**  será, em seguida, o objeto de saudação do tooserialize usado.</span><span class="sxs-lookup"><span data-stu-id="71d36-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="71d36-155">Como alternativa, um **java.io.InputStream** pode ser fornecido.</span><span class="sxs-lookup"><span data-stu-id="71d36-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="71d36-156">Olá exemplo a seguir demonstra como teste toosend cinco mensagens toothe `TestTopic` **MessageSender** obtivemos no trecho de código Olá acima.</span><span class="sxs-lookup"><span data-stu-id="71d36-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="71d36-157">Observe como Olá **MessageNumber** varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (isso determinará quais assinaturas recebem-lo):</span><span class="sxs-lookup"><span data-stu-id="71d36-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="71d36-158">Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="71d36-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="71d36-159">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="71d36-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="71d36-160">Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite no tamanho total de saudação de mensagens de saudação mantidos por um tópico.</span><span class="sxs-lookup"><span data-stu-id="71d36-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="71d36-161">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="71d36-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="71d36-162">Como tooreceive mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="71d36-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="71d36-163">tooreceive mensagens de uma assinatura, use um **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="71d36-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="71d36-164">As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="71d36-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="71d36-165">Ao usar o hello **ReceiveAndDelete** modo, recebe é uma operação de captura único - ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem, ele marca a mensagem de saudação como sendo consumida e retorna-toothe aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71d36-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="71d36-166">**ReceiveAndDelete** modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="71d36-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="71d36-167">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="71d36-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="71d36-168">Porque o barramento de serviço será marcou a mensagem como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="71d36-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="71d36-169">Em **PeekLock** , modo de recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="71d36-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="71d36-170">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71d36-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="71d36-171">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando **excluir** na mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="71d36-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="71d36-172">Quando o Service Bus vê Olá **excluir** chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo do tópico hello.</span><span class="sxs-lookup"><span data-stu-id="71d36-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="71d36-173">Olá exemplo abaixo demonstra como as mensagens podem ser recebidas e processados usando **PeekLock** modo (não o modo padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="71d36-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="71d36-174">Hello exemplo a seguir executa um loop e processa mensagens de saudação assinatura "HighMessages" e, em seguida, é encerrado quando não existem mais mensagens (como alternativa, ele pode ser definido toowait novas mensagens).</span><span class="sxs-lookup"><span data-stu-id="71d36-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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
            // Display hello topic message.
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
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="71d36-175">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="71d36-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="71d36-176">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="71d36-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="71d36-177">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **unlockMessage** método na mensagem recebida (em vez da saudação **deleteMessage** método).</span><span class="sxs-lookup"><span data-stu-id="71d36-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="71d36-178">Isso causar a mensagem de saudação do barramento de serviço toounlock tópico hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="71d36-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="71d36-179">Também há um tempo limite associado a uma mensagem bloqueada dentro do tópico, e se o aplicativo hello falhar tooprocess mensagem de saudação antes do tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), e o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="71d36-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="71d36-180">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **deleteMessage** solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="71d36-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="71d36-181">Isso é geralmente chamado **, pelo menos, após processamento**, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="71d36-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="71d36-182">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="71d36-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="71d36-183">Isso geralmente é obtido usando Olá **getMessageId** método de mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="71d36-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="71d36-184">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="71d36-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="71d36-185">Olá tópicos toodelete a principal forma e assinaturas é toouse uma **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="71d36-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="71d36-186">Excluir um tópico também excluirá quaisquer assinaturas que são registradas com o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="71d36-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="71d36-187">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="71d36-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="71d36-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71d36-188">Next Steps</span></span>
<span data-ttu-id="71d36-189">Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas do barramento de serviço, tópicos e assinaturas] [ Service Bus queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="71d36-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
