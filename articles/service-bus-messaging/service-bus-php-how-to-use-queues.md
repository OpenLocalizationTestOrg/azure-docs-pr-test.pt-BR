---
title: "filas de aaaHow toouse barramento de serviço com o PHP | Microsoft Docs"
description: "Saiba como filas de toouse barramento de serviço no Azure. Exemplos de código escritos em PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a>Como toouse Service Bus filas com PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este guia mostra como toouse filas de barramento de serviço. exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP](../php-download-sdk.md). Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Criar um aplicativo PHP
Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de Blob do Azure Olá Olá referência de classes Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro de seu código. Você pode usar qualquer toocreate de ferramentas de desenvolvimento de seu aplicativo, ou o bloco de notas.

> [!NOTE]
> A instalação do PHP também deverá ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e habilitado.
> 
> 

Neste guia, você usará os recursos de serviço que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de uma função web do Azure, função de trabalho ou no site.

## <a name="get-hello-azure-client-libraries"></a>Obter Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
fila do barramento de serviço do toouse Olá APIs, Olá a seguir:

1. Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require_once] instrução.
2. Fazer referência a qualquer classe que você possa usar.

Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático `ServicesBuilder` classe.

> [!NOTE]
> Este exemplo (e outros exemplos neste artigo) supõe que você instalou Olá PHP bibliotecas de cliente para o Azure por meio do criador. Se você instalou bibliotecas Olá manualmente ou como um pacote de PERA, você deve fazer referência a saudação **WindowsAzure.php** arquivo do carregador automático.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de saudação abaixo, Olá `require_once` instrução sempre será mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.

## <a name="set-up-a-service-bus-connection"></a>Configurar uma conexão do Barramento de Serviço
tooinstantiate um cliente do barramento de serviço, primeiro você deve ter uma cadeia de caracteres de conexão válida neste formato:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Onde `Endpoint` normalmente é do formato de saudação `[yourNamespace].servicebus.windows.net`.

toocreate qualquer cliente de serviço do Azure, você deve usar o hello `ServicesBuilder` classe. Você pode:

* Passar conexão Olá tooit cadeia de caracteres diretamente.
* Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:
  * Por padrão, ele vem com suporte para uma origem externa: variáveis de ambiente
  * Você pode adicionar novas fontes estendendo Olá `ConnectionStringSource` classe

Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão de saudação é passada diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Criar uma fila
Você pode executar operações de gerenciamento para as filas do barramento de serviço por meio de saudação `ServiceBusRestProxy` classe. Um `ServiceBusRestProxy` objeto for construído por meio de saudação `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de caracteres de conexão apropriado que encapsula Olá permissões token toomanage-lo.

Olá mostrado no exemplo a seguir como tooinstantiate uma `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createQueue` toocreate uma fila denominada `myqueue` dentro de um `MySBNamespace` namespace de serviço:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
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
> Você pode usar o hello `listQueues` método `ServiceBusRestProxy` objetos toocheck se já existe uma fila com um nome especificado em um namespace.
> 
> 

## <a name="send-messages-tooa-queue"></a>Mensagens tooa fila de envio
toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `ServiceBusRestProxy->sendQueueMessage` método. Olá mostrado no código a seguir como toosend toohello uma mensagem `myqueue` fila criada anteriormente dentro de `MySBNamespace` namespace de serviço.

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
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
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

Mensagens de filas de barramento de serviço muito enviadas (e recebidas de) são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos padrão e propriedades que são propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados arbitrários do aplicativo.

Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação. Este limite superior do tamanho da fila é 5 GB.

## <a name="receive-messages-from-a-queue"></a>Receber mensagens de uma fila

Olá melhor maneira tooreceive as mensagens de uma fila é toouse um `ServiceBusRestProxy->receiveQueueMessage` método. As mensagens podem ser recebidas de dois modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** é saudação padrão.

Ao usar [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , modo de recebimento é uma operação única etapa; ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma fila, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

No padrão de saudação [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, recebendo uma mensagem se torna uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Ao barramento de serviço recebe uma solicitação, localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores do recebimento e, em seguida, ele retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação receber o processo, passando a mensagem de saudação recebida muito`ServiceBusRestProxy->deleteMessage`. Quando o Service Bus vê Olá `deleteMessage` chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.

Olá mostrado no exemplo a seguir como tooreceive e processar uma mensagem usando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (modo de padrão de saudação).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis

Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método na mensagem recebida (em vez da saudação `deleteMessage` método). Isso causar a mensagem de saudação do barramento de serviço toounlock em fila hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e em seguida, desbloquear mensagem de saudação do barramento de serviço automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *pelo menos uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, em seguida, é recomendável adicionar a entrega de mensagens duplicadas lógica adicional tooapplications toohandle. Isso geralmente é obtido usando Olá `getMessageId` método de mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.

Para obter mais informações, visite também Olá [Centro de desenvolvedores PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


