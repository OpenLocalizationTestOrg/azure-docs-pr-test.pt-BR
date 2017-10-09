---
title: "filas de aaaHow toouse barramento de serviço no Node. js | Microsoft Docs"
description: Saiba como toouse Service Bus filas no Azure de um aplicativo Node. js.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Como toouse Service Bus filas com Node. js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artigo descreve como toouse Service Bus filas com Node. js. exemplos de saudação são escritos em JavaScript e usam Olá módulo Azure Node. js. Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**. Para obter mais informações sobre filas, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Criar um aplicativo do Node.js
Criar um aplicativo Node.js em branco. Para obter instruções sobre como toocreate um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooan site do Azure][Create and deploy a Node.js application tooan Azure Website], ou [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
toouse barramento de serviço do Azure, baixe e use Olá pacote do Azure Node. js. Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain
1. Saudação de uso **do Windows PowerShell para Node.js** comando janela toonavigate toohello **c:\\nó\\sbqueues\\WebRole1** pasta na qual você criou seu aplicativo de exemplo.
2. Tipo **npm instalar o azure** na janela de comando Olá, que deve resultar no seguinte de toohello semelhante de saída:

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. Você pode executar manualmente Olá **ls** tooverify de comando que um **node_modules** pasta foi criada. Dentro desse Olá de localizar pasta **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess filas do barramento de serviço.

### <a name="import-hello-module"></a>Módulo de saudação de importação
Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Configurar uma conexão do barramento de serviço do Azure
módulo do Azure Hello lê variável de ambiente Olá `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informações necessárias tooconnect tooService barramento. Se essa variável de ambiente não for definida, você deve especificar as informações de conta de saudação ao chamar `createServiceBusService`.

Para obter um exemplo de configuração de variáveis de ambiente Olá em um arquivo de configuração para um serviço de nuvem do Azure, consulte [Node. js serviço de nuvem com o armazenamento][Node.js Cloud Service with Storage].

Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure] [ Azure portal] para um site do Azure, consulte [aplicativo Web Node.js armazenamento] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Criar uma fila
Olá **ServiceBusService** objeto permite que você toowork com filas do barramento de serviço. Olá código a seguir cria um **ServiceBusService** objeto. Adicioná-lo superior de saudação do hello **server.js** arquivo após Olá tooimport da instrução Olá módulo do Azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Chamando `createQueueIfNotExists` em Olá **ServiceBusService** de objeto, Olá especificado fila será retornada (se houver) ou uma nova fila com o nome especificado da saudação é criada. código a seguir Olá usa `createQueueIfNotExists` toocreate ou conecte-se a fila de toohello denominada `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Olá `createServiceBusService` método também oferece suporte a opções adicionais, que permitem a você as configurações de fila de padrão de toooverride como tamanho de fila toolive ou máximo de tempo de mensagem. Olá exemplo a seguir define Olá máximo da fila tamanho too5 GB e um valor de (vida útil TTL) toolive tempo de 1 minuto:

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>Filtros
Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **ServiceBusService**. As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:

```javascript
function handle (requestOptions, next)
```

Depois de fazer seu pré-processamento nas opções de solicitação hello, deve chamar o método hello `next`, passando um retorno de chamada com hello assinatura a seguir:

```javascript
function (returnObject, finalCallback, next)
```

Em que esse retorno de chamada e depois processamento Olá `returnObject` (hello a resposta do servidor de toohello de solicitação de saudação), retorno de chamada de saudação ou deve chamar `next` se ele existe toocontinue outros filtros de processamento ou simplesmente chamar `finalCallback`, que termina invocação de serviço Hello.

Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`. Olá código a seguir cria um `ServiceBusService` objeto que usa Olá `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Mensagens tooa fila de envio
toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `sendQueueMessage` método hello **ServiceBusService** objeto. As mensagens enviadas muito (e recebidas pelo) barramento de serviço filas são **BrokeredMessage** objetos e tem um conjunto de propriedades padrão (como **rótulo** e **TimeToLive**), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir o corpo de saudação da mensagem de saudação, passando uma cadeia de caracteres como mensagem de saudação. As propriedades padrão necessárias são preenchidas com valores padrão.

Olá exemplo a seguir demonstra como toosend uma fila de toohello de mensagens de teste chamado `myqueue` usando `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação. O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB. Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).

## <a name="receive-messages-from-a-queue"></a>Receber mensagens de uma fila
As mensagens são recebidas de uma fila usando Olá `receiveQueueMessage` método hello **ServiceBusService** objeto. Por padrão, as mensagens serão excluídas da fila de saudação conforme elas são de leitura; No entanto, você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro opcional Olá configuração `isPeekLock` muito**true**.

Olá comportamento padrão de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Se hello `isPeekLock` parâmetro está definido muito**true**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `deleteMessage` método e fornecendo toobe de mensagem de saudação excluído como um parâmetro. Olá `deleteMessage` método marca a mensagem de saudação como sendo consumida e remove da fila de saudação.

Olá exemplo a seguir demonstra como tooreceive e processar mensagens usando `receiveQueueMessage`. Olá exemplo primeiro recebe e exclui uma mensagem e, em seguida, recebe uma mensagem usando `isPeekLock` definido muito**true**, em seguida, exclui hello usando `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método hello **ServiceBusService** objeto. Isso causar toounlock do barramento de serviço a mensagem na fila de saudação e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se Olá falha de aplicativo hello tooprocess Olá mensagem antes de tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre as filas, consulte Olá recursos a seguir.

* [Filas, tópicos e assinaturas][Queues, topics, and subscriptions]
* Repositório do [SDK do Azure para Node][Azure SDK for Node] no GitHub
* [Centro de desenvolvedores do Node. js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
