---
title: "Como usar os tópicos de Barramento de Serviço com PHP | Microsoft Docs"
description: "Saiba como usar tópicos do Barramento de Serviço com PHP no Azure."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="6355e-103">Como usar tópicos e assinaturas do Barramento de Serviço com PHP</span><span class="sxs-lookup"><span data-stu-id="6355e-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="6355e-104">Este artigo mostra como usar os tópicos e as assinaturas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6355e-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="6355e-105">As amostras são escritas em PHP e usam o [SDK do Azure para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6355e-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="6355e-106">Os cenários abordados incluem a **criação de tópicos e assinaturas**, a **criação de filtros de assinatura**, o **envio de mensagens para um tópico**, o **recebimento de mensagens de uma assinatura** e a **exclusão de tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="6355e-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="6355e-107">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="6355e-107">Create a PHP application</span></span>
<span data-ttu-id="6355e-108">O único requisito para a criação de um aplicativo PHP que acessa o serviço Blob do Azure é a referência de classes no [SDK do Azure para PHP](../php-download-sdk.md) em seu código.</span><span class="sxs-lookup"><span data-stu-id="6355e-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="6355e-109">Você pode usar quaisquer ferramentas de desenvolvimento para criar seu aplicativo, ou o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="6355e-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="6355e-110">A instalação do PHP também deve ter a [extensão OpenSSL](http://php.net/openssl) instalada e habilitada.</span><span class="sxs-lookup"><span data-stu-id="6355e-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="6355e-111">Este artigo descreve como usar os recursos de serviços que podem ser chamados em um aplicativo PHP localmente ou no código em execução em uma função web, uma função de trabalho ou um site do Azure.</span><span class="sxs-lookup"><span data-stu-id="6355e-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="6355e-112">Obter as bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="6355e-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="6355e-113">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="6355e-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="6355e-114">Para usar as APIs do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="6355e-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="6355e-115">Faça referência ao arquivo do carregador automático usando a instrução [require_once][require-once].</span><span class="sxs-lookup"><span data-stu-id="6355e-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="6355e-116">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="6355e-116">Reference any classes you might use.</span></span>

<span data-ttu-id="6355e-117">O exemplo a seguir mostra como incluir o arquivo de carregador automático e fazer referência à classe **ServicesBuilder**.</span><span class="sxs-lookup"><span data-stu-id="6355e-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="6355e-118">Este exemplo (e outros exemplos neste artigo) pressupõe que você instalou as Bibliotecas de Cliente PHP para Azure por meio do Compositor.</span><span class="sxs-lookup"><span data-stu-id="6355e-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="6355e-119">Se você instalou as bibliotecas manualmente ou como um pacote PEAR, será necessário fazer referência ao arquivo de carregador automático **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="6355e-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="6355e-120">Nos seguintes exemplos, a instrução `require_once` será mostrada sempre, mas somente as classes necessárias para executar o exemplo serão referenciadas.</span><span class="sxs-lookup"><span data-stu-id="6355e-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="6355e-121">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6355e-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="6355e-122">Para criar uma instância do cliente do Barramento de Serviço, você deve ter primeiro uma cadeia de conexão válida neste formato:</span><span class="sxs-lookup"><span data-stu-id="6355e-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="6355e-123">Em que `Endpoint` geralmente está no formato `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="6355e-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="6355e-124">Para criar um cliente de serviço do Azure, é necessário usar a classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="6355e-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="6355e-125">Você pode:</span><span class="sxs-lookup"><span data-stu-id="6355e-125">You can:</span></span>

* <span data-ttu-id="6355e-126">Passar a cadeia de conexão diretamente para ele.</span><span class="sxs-lookup"><span data-stu-id="6355e-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="6355e-127">Usar **CloudConfigurationManager (CCM)** para verificar várias fontes externas da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="6355e-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="6355e-128">Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="6355e-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="6355e-129">Você pode adicionar novas origens estendendo a classe `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="6355e-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="6355e-130">Para os exemplos descritos aqui, a cadeia de conexão é passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="6355e-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="6355e-131">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="6355e-131">Create a topic</span></span>
<span data-ttu-id="6355e-132">Você pode executar operações de gerenciamento de tópicos do Barramento de Serviço por meio da classe `ServiceBusRestProxy` .</span><span class="sxs-lookup"><span data-stu-id="6355e-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="6355e-133">Um objeto `ServiceBusRestProxy` é construído com o método de fábrica `ServicesBuilder::createServiceBusService` com uma cadeia de conexão apropriada que encapsula as permissões de token para gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="6355e-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="6355e-134">O exemplo a seguir mostra como instanciar um `ServiceBusRestProxy` e chamar um `ServiceBusRestProxy->createTopic` para criar um tópico denominado `mytopic` dentro de um namespace `MySBNamespace`:</span><span class="sxs-lookup"><span data-stu-id="6355e-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="6355e-135">Você pode usar o método `listTopics` em objetos `ServiceBusRestProxy` para verificar se já existe um tópico com um nome especificado em um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="6355e-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="6355e-136">Criar uma assinatura</span><span class="sxs-lookup"><span data-stu-id="6355e-136">Create a subscription</span></span>
<span data-ttu-id="6355e-137">As assinaturas do tópico também são criadas com o método `ServiceBusRestProxy->createSubscription`.</span><span class="sxs-lookup"><span data-stu-id="6355e-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="6355e-138">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de mensagens passadas para a fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="6355e-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="6355e-139">Criar uma assinatura com o filtro padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="6355e-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="6355e-140">O filtro **MatchAll** será o padrão usado se nenhum filtro for especificado quando uma nova assinatura for criada.</span><span class="sxs-lookup"><span data-stu-id="6355e-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="6355e-141">Quando o filtro **MatchAll** é usado, todas as mensagens publicadas no tópico são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="6355e-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="6355e-142">O exemplo a seguir cria uma assinatura denominada 'mysubscription' e usa o filtro padrão **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="6355e-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="6355e-143">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="6355e-143">Create subscriptions with filters</span></span>
<span data-ttu-id="6355e-144">Você também pode configurar filtros que permitem especificar quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica do tópico.</span><span class="sxs-lookup"><span data-stu-id="6355e-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="6355e-145">O tipo de filtro mais flexível compatível com as assinaturas é o [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="6355e-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="6355e-146">Os filtros SQL operam nas propriedades das mensagens que são publicadas no tópico.</span><span class="sxs-lookup"><span data-stu-id="6355e-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="6355e-147">Para saber mais sobre SqlFilters, consulte [Propriedade SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="6355e-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="6355e-148">Cada regra uma assinatura processa as mensagens de entrada independentemente, adicionando suas mensagens de resultado à assinatura.</span><span class="sxs-lookup"><span data-stu-id="6355e-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="6355e-149">Além disso, cada nova assinatura tem um objeto **Regra** padrão com um filtro que adiciona todas as mensagens do tópico à assinatura.</span><span class="sxs-lookup"><span data-stu-id="6355e-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="6355e-150">Para receber apenas as mensagens correspondentes ao filtro, você deve remover a regra padrão.</span><span class="sxs-lookup"><span data-stu-id="6355e-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="6355e-151">Você pode remover a regra padrão usando o método `ServiceBusRestProxy->deleteRule`.</span><span class="sxs-lookup"><span data-stu-id="6355e-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="6355e-152">O exemplo a seguir cria uma assinatura denominada `HighMessages` com um **SqlFilter** que seleciona apenas as mensagens que tenham uma propriedade personalizada `MessageNumber` maior que 3.</span><span class="sxs-lookup"><span data-stu-id="6355e-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="6355e-153">Confira [Enviar mensagens para um tópico](#send-messages-to-a-topic) para saber mais sobre como adicionar propriedades a mensagens.</span><span class="sxs-lookup"><span data-stu-id="6355e-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="6355e-154">Observe que este código requer o uso de um namespace adicional: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="6355e-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="6355e-155">Da mesma forma, o seguinte exemplo cria uma assinatura denominada `LowMessages` com um `SqlFilter` que seleciona apenas mensagens que têm uma propriedade `MessageNumber` menor ou igual a 3.</span><span class="sxs-lookup"><span data-stu-id="6355e-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="6355e-156">Agora, quando uma mensagem é enviada ao tópico `mytopic`, ela sempre será entregue aos destinatários inscritos na assinatura `mysubscription` e entregue de forma seletiva aos destinatários inscritos nas assinaturas do `HighMessages` e `LowMessages` (dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="6355e-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="6355e-157">Enviar mensagens para um tópico</span><span class="sxs-lookup"><span data-stu-id="6355e-157">Send messages to a topic</span></span>
<span data-ttu-id="6355e-158">Para enviar uma mensagem para um tópico do Barramento de Serviço, seu aplicativo chamará o método `ServiceBusRestProxy->sendTopicMessage`.</span><span class="sxs-lookup"><span data-stu-id="6355e-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="6355e-159">O código abaixo demonstra como enviar uma mensagem ao tópico `mytopic` que criamos acima no namespace de serviço `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="6355e-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="6355e-160">As mensagens enviadas aos tópicos do Barramento de Serviço são instâncias da classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="6355e-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="6355e-161">Os objetos [BrokeredMessage][BrokeredMessage] têm um conjunto de propriedades e métodos padrão, além de propriedades que podem ser usadas para manter as propriedades personalizadas específicas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6355e-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="6355e-162">O exemplo a seguir mostra como enviar cinco mensagens de teste para o tópico `mytopic` criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6355e-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="6355e-163">O método `setProperty` é usado para adicionar uma propriedade personalizada (`MessageNumber`) a cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="6355e-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="6355e-164">Observe como o valor da propriedade `MessageNumber` varia em cada mensagem (ele pode ser usado para determinar quais assinaturas o receberão, conforme mostrado na seção [Criar uma assinatura](#create-a-subscription)):</span><span class="sxs-lookup"><span data-stu-id="6355e-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="6355e-165">Os tópicos do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6355e-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="6355e-166">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6355e-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="6355e-167">Não há nenhum limite no número de mensagens mantidas em um tópico, mas há uma capacidade do tamanho total das mensagens mantidas por um tópico.</span><span class="sxs-lookup"><span data-stu-id="6355e-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="6355e-168">Este limite superior do tamanho do tópico é 5 GB.</span><span class="sxs-lookup"><span data-stu-id="6355e-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="6355e-169">Para saber mais sobre cotas, consulte [Cotas do Barramento de Serviço][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="6355e-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="6355e-170">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="6355e-170">Receive messages from a subscription</span></span>
<span data-ttu-id="6355e-171">A maneira mais fácil de receber mensagens de uma assinatura é usar um método `ServiceBusRestProxy->receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="6355e-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="6355e-172">As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="6355e-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="6355e-173">**PeekLock** é o padrão.</span><span class="sxs-lookup"><span data-stu-id="6355e-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="6355e-174">Quando o modo [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) for usado, o recebimento será uma operação única, ou seja, quando o Barramento de Serviço receber uma solicitação de leitura de uma mensagem em uma assinatura, ele marcará a mensagem como sendo consumida e a retornará ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6355e-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="6355e-175">O modo [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo pode tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="6355e-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="6355e-176">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="6355e-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="6355e-177">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="6355e-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="6355e-178">No modo [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) padrão, o recebimento de uma mensagem se torna uma operação de dois estágios, o que possibilita o suporte a aplicativos que não podem tolerar ausência de mensagens.</span><span class="sxs-lookup"><span data-stu-id="6355e-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="6355e-179">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6355e-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="6355e-180">Depois que o aplicativo conclui o processamento da mensagem (ou a armazena de forma segura para processamento futuro), ele conclui a segunda etapa do processo de recebimento encaminhando a mensagem recebida para `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="6355e-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="6355e-181">Quando o Barramento de Serviço vê a chamada `deleteMessage`, ele marca a mensagem como tendo sido consumida e a remove da fila.</span><span class="sxs-lookup"><span data-stu-id="6355e-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="6355e-182">O exemplo a seguir mostra como receber e processar uma mensagem usando o modo [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (o modo padrão).</span><span class="sxs-lookup"><span data-stu-id="6355e-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="6355e-183">Como: tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="6355e-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="6355e-184">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6355e-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="6355e-185">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele poderá chamar o método `unlockMessage` na mensagem recebida (em vez do método `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="6355e-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="6355e-186">Isso fará com que o Service Bus desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="6355e-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="6355e-187">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se o aplicativo não conseguir processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, em caso de falha do aplicativo), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="6355e-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="6355e-188">Se houver falha do aplicativo após o processamento da mensagem, mas antes que a solicitação `deleteMessage` seja gerada, a mensagem será entregue novamente ao aplicativo quando ele reiniciar.</span><span class="sxs-lookup"><span data-stu-id="6355e-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="6355e-189">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez, mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="6355e-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="6355e-190">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra aos aplicativos para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="6355e-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="6355e-191">Isso geralmente é realizado usando o método `getMessageId` da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="6355e-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="6355e-192">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="6355e-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="6355e-193">Para excluir um tópico ou uma assinatura, use os métodos `ServiceBusRestProxy->deleteTopic` ou `ServiceBusRestProxy->deleteSubscripton`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6355e-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="6355e-194">Observe que a exclusão de um tópico também exclui todas as assinaturas registradas com o tópico.</span><span class="sxs-lookup"><span data-stu-id="6355e-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="6355e-195">O exemplo a seguir mostra como excluir um tópico denominado `mytopic` e suas assinaturas registradas.</span><span class="sxs-lookup"><span data-stu-id="6355e-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="6355e-196">Ao usar o método `deleteSubscription`, você poderá excluir uma assinatura de forma independente:</span><span class="sxs-lookup"><span data-stu-id="6355e-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="6355e-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6355e-197">Next steps</span></span>
<span data-ttu-id="6355e-198">Agora que você aprendeu as noções básicas sobre as filas do Barramento de Serviço, veja [Filas, tópicos e assinaturas][Queues, topics, and subscriptions] para saber mais.</span><span class="sxs-lookup"><span data-stu-id="6355e-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
