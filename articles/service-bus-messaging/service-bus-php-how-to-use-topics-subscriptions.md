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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Como toouse Service Bus tópicos e assinaturas com PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artigo mostra como toouse Service Bus tópicos e assinaturas. exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP](../php-download-sdk.md). Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Criar um aplicativo PHP
Olá somente requisito para criar um aplicativo PHP que acessa o serviço de Blob do Azure Olá é tooreference classes Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro de seu código. Você pode usar qualquer toocreate de ferramentas de desenvolvimento de seu aplicativo, ou o bloco de notas.

> [!NOTE]
> A instalação do PHP também deverá ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e habilitado.
> 
> 

Este artigo descreve como toouse serviço recursos que podem ser chamados dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, uma função de trabalho ou um site.

## <a name="get-hello-azure-client-libraries"></a>Obter Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
Olá toouse APIs do barramento de serviço:

1. Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require-once] instrução.
2. Fazer referência a qualquer classe que você possa usar.

Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServiceBusService** classe.

> [!NOTE]
> Este exemplo (e outros exemplos neste artigo) supõe que você instalou Olá PHP bibliotecas de cliente para o Azure por meio do criador. Se você instalou bibliotecas Olá manualmente ou como um pacote de PERA, você deve fazer referência a saudação **WindowsAzure.php** arquivo do carregador automático.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos a seguir de hello, Olá `require_once` instrução sempre será mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.

## <a name="set-up-a-service-bus-connection"></a>Configurar uma conexão do Barramento de Serviço
tooinstantiate um cliente de barramento de serviço, você deve primeiro ter uma cadeia de caracteres de conexão válida neste formato:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Onde `Endpoint` normalmente é do formato de saudação `https://[yourNamespace].servicebus.windows.net`.

toocreate qualquer cliente de serviço do Azure, você deve usar o hello `ServicesBuilder` classe. Você pode:

* Passar conexão Olá tooit cadeia de caracteres diretamente.
* Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:
  * Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente
  * Você pode adicionar novas fontes estendendo Olá `ConnectionStringSource` classe.

Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão de saudação é passada diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Criar um tópico
Você pode executar operações de gerenciamento para os tópicos do barramento de serviço por meio de saudação `ServiceBusRestProxy` classe. Um `ServiceBusRestProxy` objeto for construído por meio de saudação `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de caracteres de conexão apropriado que encapsula Olá permissões token toomanage-lo.

Olá mostrado no exemplo a seguir como tooinstantiate uma `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createTopic` toocreate um tópico chamado `mytopic` dentro de um `MySBNamespace` namespace:

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
> Você pode usar o hello `listTopics` método `ServiceBusRestProxy` objetos toocheck se um tópico com um nome especificado já existe em um namespace de serviço.
> 
> 

## <a name="create-a-subscription"></a>Criar uma assinatura
Assinaturas de tópico também são criadas com hello `ServiceBusRestProxy->createSubscription` método. As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens passado a fila virtual toohello da assinatura.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma assinatura com o filtro saudação padrão (MatchAll)
Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada. Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello. Olá, exemplo a seguir cria uma assinatura chamada 'mysubscription' e usa Olá padrão **MatchAll** filtro.

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

### <a name="create-subscriptions-with-filters"></a>Criar assinaturas com os filtros
Você também pode definir os filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve aparecer dentro de uma assinatura de tópico específico. Olá, mais flexível tipo de filtro de assinaturas com suporte é Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), que implementa um subconjunto do SQL92. Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico. Para saber mais sobre SqlFilters, consulte [Propriedade SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Cada regra em uma assinatura processa mensagens de entrada de forma independente, adicionando sua assinatura de toohello de mensagens de resultados. Além disso, cada nova assinatura tem um padrão **regra** objeto com um filtro que adiciona todas as mensagens de saudação tópico toohello assinatura. tooreceive somente as mensagens que correspondem o filtro, você deve remover a regra padrão de saudação. Você pode remover a regra padrão de saudação usando Olá `ServiceBusRestProxy->deleteRule` método.
> 
> 

Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `MessageNumber` propriedade maior que 3. Consulte [tópico de tooa enviar mensagens](#send-messages-to-a-topic) para obter informações sobre como adicionar propriedades personalizadas toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Observe que esse código requer o uso de saudação de um namespace adicional: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um `SqlFilter` que seleciona somente as mensagens que têm um `MessageNumber` propriedade menor ou igual too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Agora, quando uma mensagem é enviada toohello `mytopic` tópico, ele é sempre entregue tooreceivers inscrito toohello `mysubscription` assinatura e tooreceivers seletivamente entregue inscrito toohello `HighMessages` e `LowMessages` (assinaturas Dependendo de conteúdo da mensagem de saudação).

## <a name="send-messages-tooa-topic"></a>Enviar tópico tooa de mensagens
toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo chama Olá `ServiceBusRestProxy->sendTopicMessage` método. Olá o seguinte código mostra como toosend toohello uma mensagem `mytopic` tópico previamente criado dentro de `MySBNamespace` namespace de serviço.

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

As mensagens enviadas tooService tópicos do barramento são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos e propriedades padrão, bem como propriedades que podem ser usados toohold propriedades personalizadas da específicas do aplicativo. Olá exemplo a seguir mostra como as mensagens de teste de toosend 5 toohello `mytopic` tópico criado anteriormente. Olá `setProperty` método é usado tooadd uma propriedade personalizada (`MessageNumber`) tooeach mensagem. Observe que Olá `MessageNumber` varia de acordo com o valor da propriedade em cada mensagem (você pode usar este toodetermine valor quais assinaturas recebem-lo, conforme mostrado no hello [criar uma assinatura](#create-a-subscription) seção):

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

Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico. Este limite superior do tamanho do tópico é 5 GB. Para saber mais sobre cotas, consulte [Cotas do Barramento de Serviço][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma assinatura
Olá melhor maneira tooreceive as mensagens de uma assinatura é toouse um `ServiceBusRestProxy->receiveSubscriptionMessage` método. As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** é saudação padrão.

Ao usar o hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , modo de recebimento é uma operação única etapa; ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma assinatura, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

No padrão de saudação [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, recebendo uma mensagem se torna uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber o processo, passando a mensagem de saudação recebida muito`ServiceBusRestProxy->deleteMessage`. Quando o Service Bus vê Olá `deleteMessage` chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.

Olá mostrado no exemplo a seguir como tooreceive e processar uma mensagem usando [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (modo de padrão de saudação). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Como: tratar falhas do aplicativo e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método na mensagem recebida (em vez da saudação `deleteMessage` método). Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *pelo menos uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tooapplications toohandle. Isso geralmente é obtido usando Olá `getMessageId` método de mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Excluir tópicos e assinaturas
toodelete um tópico ou uma assinatura, use Olá `ServiceBusRestProxy->deleteTopic` ou hello `ServiceBusRestProxy->deleteSubscripton` métodos, respectivamente. Observe que a exclusão de um tópico também exclui quaisquer assinaturas que são registradas com o tópico de saudação.

Olá exemplo a seguir mostra como toodelete um tópico chamado `mytopic` e suas assinaturas registradas.

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

Usando Olá `deleteSubscription` método, você pode excluir uma assinatura de forma independente:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
