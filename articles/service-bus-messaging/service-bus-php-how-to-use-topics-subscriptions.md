---
title: "tópicos do barramento de serviço do toouse aaaHow com PHP | Microsoft Docs"
description: "Saiba como toouse tópicos de barramento de serviço com o PHP no Azure."
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
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="e9991-103">Como toouse Service Bus tópicos e assinaturas com PHP</span><span class="sxs-lookup"><span data-stu-id="e9991-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="e9991-104">Este artigo mostra como toouse Service Bus tópicos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e9991-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="e9991-105">exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e9991-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="e9991-106">Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="e9991-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e9991-107">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="e9991-107">Create a PHP application</span></span>
<span data-ttu-id="e9991-108">Olá somente requisito para criar um aplicativo PHP que acessa o serviço de Blob do Azure Olá é tooreference classes Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="e9991-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="e9991-109">Você pode usar qualquer toocreate de ferramentas de desenvolvimento de seu aplicativo, ou o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="e9991-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="e9991-110">A instalação do PHP também deverá ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="e9991-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="e9991-111">Este artigo descreve como toouse serviço recursos que podem ser chamados dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, uma função de trabalho ou um site.</span><span class="sxs-lookup"><span data-stu-id="e9991-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="e9991-112">Obter Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="e9991-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="e9991-113">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e9991-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="e9991-114">Olá toouse APIs do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="e9991-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="e9991-115">Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require-once] instrução.</span><span class="sxs-lookup"><span data-stu-id="e9991-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="e9991-116">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="e9991-116">Reference any classes you might use.</span></span>

<span data-ttu-id="e9991-117">Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="e9991-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="e9991-118">Este exemplo (e outros exemplos neste artigo) supõe que você instalou Olá PHP bibliotecas de cliente para o Azure por meio do criador.</span><span class="sxs-lookup"><span data-stu-id="e9991-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e9991-119">Se você instalou bibliotecas Olá manualmente ou como um pacote de PERA, você deve fazer referência a saudação **WindowsAzure.php** arquivo do carregador automático.</span><span class="sxs-lookup"><span data-stu-id="e9991-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="e9991-120">Nos exemplos a seguir de hello, Olá `require_once` instrução sempre será mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="e9991-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="e9991-121">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e9991-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="e9991-122">tooinstantiate um cliente de barramento de serviço, você deve primeiro ter uma cadeia de caracteres de conexão válida neste formato:</span><span class="sxs-lookup"><span data-stu-id="e9991-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="e9991-123">Onde `Endpoint` normalmente é do formato de saudação `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e9991-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="e9991-124">toocreate qualquer cliente de serviço do Azure, você deve usar o hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="e9991-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="e9991-125">Você pode:</span><span class="sxs-lookup"><span data-stu-id="e9991-125">You can:</span></span>

* <span data-ttu-id="e9991-126">Passar conexão Olá tooit cadeia de caracteres diretamente.</span><span class="sxs-lookup"><span data-stu-id="e9991-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="e9991-127">Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="e9991-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="e9991-128">Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="e9991-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="e9991-129">Você pode adicionar novas fontes estendendo Olá `ConnectionStringSource` classe.</span><span class="sxs-lookup"><span data-stu-id="e9991-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="e9991-130">Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão de saudação é passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="e9991-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="e9991-131">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="e9991-131">Create a topic</span></span>
<span data-ttu-id="e9991-132">Você pode executar operações de gerenciamento para os tópicos do barramento de serviço por meio de saudação `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="e9991-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="e9991-133">Um `ServiceBusRestProxy` objeto for construído por meio de saudação `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de caracteres de conexão apropriado que encapsula Olá permissões token toomanage-lo.</span><span class="sxs-lookup"><span data-stu-id="e9991-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="e9991-134">Olá mostrado no exemplo a seguir como tooinstantiate uma `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createTopic` toocreate um tópico chamado `mytopic` dentro de um `MySBNamespace` namespace:</span><span class="sxs-lookup"><span data-stu-id="e9991-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="e9991-135">Você pode usar o hello `listTopics` método `ServiceBusRestProxy` objetos toocheck se um tópico com um nome especificado já existe em um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="e9991-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="e9991-136">Criar uma assinatura</span><span class="sxs-lookup"><span data-stu-id="e9991-136">Create a subscription</span></span>
<span data-ttu-id="e9991-137">Assinaturas de tópico também são criadas com hello `ServiceBusRestProxy->createSubscription` método.</span><span class="sxs-lookup"><span data-stu-id="e9991-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="e9991-138">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens passado a fila virtual toohello da assinatura.</span><span class="sxs-lookup"><span data-stu-id="e9991-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="e9991-139">Criar uma assinatura com o filtro saudação padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="e9991-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="e9991-140">Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada.</span><span class="sxs-lookup"><span data-stu-id="e9991-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="e9991-141">Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="e9991-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="e9991-142">Olá, exemplo a seguir cria uma assinatura chamada 'mysubscription' e usa Olá padrão **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="e9991-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="e9991-143">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="e9991-143">Create subscriptions with filters</span></span>
<span data-ttu-id="e9991-144">Você também pode definir os filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve aparecer dentro de uma assinatura de tópico específico.</span><span class="sxs-lookup"><span data-stu-id="e9991-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="e9991-145">Olá, mais flexível tipo de filtro de assinaturas com suporte é Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="e9991-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="e9991-146">Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="e9991-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="e9991-147">Para saber mais sobre SqlFilters, consulte [Propriedade SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="e9991-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="e9991-148">Cada regra em uma assinatura processa mensagens de entrada de forma independente, adicionando sua assinatura de toohello de mensagens de resultados.</span><span class="sxs-lookup"><span data-stu-id="e9991-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="e9991-149">Além disso, cada nova assinatura tem um padrão **regra** objeto com um filtro que adiciona todas as mensagens de saudação tópico toohello assinatura.</span><span class="sxs-lookup"><span data-stu-id="e9991-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="e9991-150">tooreceive somente as mensagens que correspondem o filtro, você deve remover a regra padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9991-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="e9991-151">Você pode remover a regra padrão de saudação usando Olá `ServiceBusRestProxy->deleteRule` método.</span><span class="sxs-lookup"><span data-stu-id="e9991-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="e9991-152">Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `MessageNumber` propriedade maior que 3.</span><span class="sxs-lookup"><span data-stu-id="e9991-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="e9991-153">Consulte [tópico de tooa enviar mensagens](#send-messages-to-a-topic) para obter informações sobre como adicionar propriedades personalizadas toomessages.</span><span class="sxs-lookup"><span data-stu-id="e9991-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="e9991-154">Observe que esse código requer o uso de saudação de um namespace adicional: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="e9991-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="e9991-155">Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um `SqlFilter` que seleciona somente as mensagens que têm um `MessageNumber` propriedade menor ou igual too3.</span><span class="sxs-lookup"><span data-stu-id="e9991-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="e9991-156">Agora, quando uma mensagem é enviada toohello `mytopic` tópico, ele é sempre entregue tooreceivers inscrito toohello `mysubscription` assinatura e tooreceivers seletivamente entregue inscrito toohello `HighMessages` e `LowMessages` (assinaturas Dependendo de conteúdo da mensagem de saudação).</span><span class="sxs-lookup"><span data-stu-id="e9991-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="e9991-157">Enviar tópico tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="e9991-157">Send messages tooa topic</span></span>
<span data-ttu-id="e9991-158">toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo chama Olá `ServiceBusRestProxy->sendTopicMessage` método.</span><span class="sxs-lookup"><span data-stu-id="e9991-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="e9991-159">Olá o seguinte código mostra como toosend toohello uma mensagem `mytopic` tópico previamente criado dentro de `MySBNamespace` namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="e9991-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="e9991-160">As mensagens enviadas tooService tópicos do barramento são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="e9991-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="e9991-161">[BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos e propriedades padrão, bem como propriedades que podem ser usados toohold propriedades personalizadas da específicas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9991-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="e9991-162">Olá exemplo a seguir mostra como as mensagens de teste de toosend 5 toohello `mytopic` tópico criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e9991-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="e9991-163">Olá `setProperty` método é usado tooadd uma propriedade personalizada (`MessageNumber`) tooeach mensagem.</span><span class="sxs-lookup"><span data-stu-id="e9991-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="e9991-164">Observe que Olá `MessageNumber` varia de acordo com o valor da propriedade em cada mensagem (você pode usar este toodetermine valor quais assinaturas recebem-lo, conforme mostrado no hello [criar uma assinatura](#create-a-subscription) seção):</span><span class="sxs-lookup"><span data-stu-id="e9991-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="e9991-165">Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e9991-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e9991-166">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="e9991-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e9991-167">Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico.</span><span class="sxs-lookup"><span data-stu-id="e9991-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="e9991-168">Este limite superior do tamanho do tópico é 5 GB.</span><span class="sxs-lookup"><span data-stu-id="e9991-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="e9991-169">Para saber mais sobre cotas, consulte [Cotas do Barramento de Serviço][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="e9991-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="e9991-170">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="e9991-170">Receive messages from a subscription</span></span>
<span data-ttu-id="e9991-171">Olá melhor maneira tooreceive as mensagens de uma assinatura é toouse um `ServiceBusRestProxy->receiveSubscriptionMessage` método.</span><span class="sxs-lookup"><span data-stu-id="e9991-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="e9991-172">As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="e9991-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="e9991-173">**PeekLock** é saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e9991-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="e9991-174">Ao usar o hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , modo de recebimento é uma operação única etapa; ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma assinatura, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9991-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="e9991-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="e9991-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="e9991-176">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="e9991-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="e9991-177">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="e9991-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="e9991-178">No padrão de saudação [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, recebendo uma mensagem se torna uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="e9991-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e9991-179">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9991-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="e9991-180">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber o processo, passando a mensagem de saudação recebida muito`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="e9991-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="e9991-181">Quando o Service Bus vê Olá `deleteMessage` chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9991-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="e9991-182">Olá mostrado no exemplo a seguir como tooreceive e processar uma mensagem usando [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (modo de padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="e9991-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e9991-183">Como: tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="e9991-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="e9991-184">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="e9991-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e9991-185">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método na mensagem recebida (em vez da saudação `deleteMessage` método).</span><span class="sxs-lookup"><span data-stu-id="e9991-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="e9991-186">Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="e9991-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e9991-187">Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="e9991-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="e9991-188">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="e9991-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="e9991-189">Isso é geralmente chamado *pelo menos uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="e9991-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="e9991-190">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tooapplications toohandle.</span><span class="sxs-lookup"><span data-stu-id="e9991-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="e9991-191">Isso geralmente é obtido usando Olá `getMessageId` método de mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="e9991-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="e9991-192">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="e9991-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="e9991-193">toodelete um tópico ou uma assinatura, use Olá `ServiceBusRestProxy->deleteTopic` ou hello `ServiceBusRestProxy->deleteSubscripton` métodos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e9991-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="e9991-194">Observe que a exclusão de um tópico também exclui quaisquer assinaturas que são registradas com o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9991-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="e9991-195">Olá exemplo a seguir mostra como toodelete um tópico chamado `mytopic` e suas assinaturas registradas.</span><span class="sxs-lookup"><span data-stu-id="e9991-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="e9991-196">Usando Olá `deleteSubscription` método, você pode excluir uma assinatura de forma independente:</span><span class="sxs-lookup"><span data-stu-id="e9991-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="e9991-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9991-197">Next steps</span></span>
<span data-ttu-id="e9991-198">Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e9991-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
