---
title: "aaaHow toouse Azure Service Bus tópicos e assinaturas com Node. js | Microsoft Docs"
description: "Saiba como toouse Service Bus tópicos e assinaturas no Azure de um aplicativo Node. js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Como tooUse Service Bus tópicos e assinaturas com Node. js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este guia descreve como toouse Service Bus tópicos e assinaturas de aplicativos Node. js. Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **enviando mensagens** tooa tópico **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**. Para obter mais informações sobre tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Criar um aplicativo do Node.js
Criar um aplicativo Node.js em branco. Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooan Site do Azure], [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell, ou Site da Web com o WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
toouse barramento de serviço, baixe Olá pacote do Azure Node. js. Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue toohello pasta em que você criou o aplicativo de exemplo.
2. Tipo **npm instalar o azure** na janela de comando hello, que deve resultar em Olá saída a seguir:

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
3. Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta encontrar o **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess tópicos do barramento de serviço.

### <a name="import-hello-module"></a>Módulo de saudação de importação
Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Configurar uma conexão do Barramento de Serviço
módulo do Azure Hello lê as variáveis de ambiente Olá `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` para obter informações necessárias tooconnect tooService barramento. Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar `createServiceBusService`.

Para obter um exemplo de configuração de variáveis de ambiente Olá para um serviço de nuvem do Azure, consulte [Node. js serviço de nuvem com o armazenamento][Node.js Cloud Service with Storage].

Para obter um exemplo de configuração de variáveis de ambiente Olá para um site do Azure, consulte [aplicativo Web Node.js armazenamento][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Criar um tópico
Olá **ServiceBusService** objeto permite que você toowork com tópicos. O código a seguir cria um objeto **ServiceBusService**. Adicioná-lo na parte superior da saudação **server.js** arquivo depois de módulo de saudação do azure Olá instrução tooimport:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Chamando `createTopicIfNotExists` em Olá **ServiceBusService** do objeto, Olá especificado tópico será retornado (se houver), ou será criado um novo tópico com o nome especificado da saudação. código a seguir Olá usa `createTopicIfNotExists` toocreate ou conecte-se toohello tópico chamado `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Olá `createServiceBusService` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações do tópico como vida útil da mensagem ou o tamanho máximo do tópico. Olá exemplo a seguir define Olá too5GB de tamanho máximo do tópico com um tempo toolive de 1 minuto:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtros
Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **ServiceBusService**. As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:

```javascript
function handle (requestOptions, next)
```

Depois de executar o pré-processamento nas opções de solicitação hello, Olá chamadas de método `next`, passando um retorno de chamada com hello assinatura a seguir:

```javascript
function (returnObject, finalCallback, next)
```

Nesse retorno de chamada e depois processamento Olá `returnObject` (hello a resposta do servidor de toohello de solicitação de saudação), precisa de retorno de chamada hello tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou invocar `finalCallback` Olá de tooend caso contrário, invocação de serviço.

Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Olá seguir cria um **ServiceBusService** objeto que usa Olá **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Criar assinaturas
Assinaturas de tópico também são criadas com hello **ServiceBusService** objeto. As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.

> [!NOTE]
> Assinaturas são persistentes e continuarão tooexist até a eles ou hello tópico eles estão associados são excluídos. Se seu aplicativo contiver lógica toocreate uma assinatura, ele deve primeiro verificar se a assinatura de saudação já existe usando o `getSubscription` método.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma assinatura com o filtro saudação padrão (MatchAll)
Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada. Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas na fila virtual da assinatura. Olá, exemplo a seguir cria uma assinatura chamada 'AllMessages' e usa Olá padrão **MatchAll** filtro.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Criar assinaturas com os filtros
Você também pode criar filtros que permitem que você tooscope quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.

Hello mais flexível o tipo de filtro de assinaturas com suporte é o **SqlFilter**, que implementa um subconjunto do SQL92. Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico. Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.

Filtros podem ser adicionados a assinatura tooa usando Olá `createRule` método hello **ServiceBusService** objeto. Esse método permite que você adicionar nova assinatura existente tooan de filtros.

> [!NOTE]
> Porque o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou **MatchAll** substituirá os outros filtros que você pode especificar. Você pode remover a regra padrão de saudação usando Olá `deleteRule` método o **ServiceBusService** objeto.
>
>

Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `messagenumber` propriedade maior que 3:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um `messagenumber` propriedade menor ou igual too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Quando uma mensagem agora é enviada muito`MyTopic`, ele sempre será entregue aos destinatários inscrito toohello `AllMessages` assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello `HighMessages` e `LowMessages` assinaturas de tópico (dependendo de conteúdo da mensagem de saudação).

## <a name="how-toosend-messages-tooa-topic"></a>Como as mensagens de toosend tooa tópico
toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar o `sendTopicMessage` método hello **ServiceBusService** objeto.
As mensagens enviadas são tópicos do barramento tooService **BrokeredMessage** objetos.
**BrokeredMessage** objetos têm um conjunto de propriedades padrão (como `Label` e `TimeToLive`), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados de cadeia de caracteres. Um aplicativo pode definir o corpo de saudação da mensagem de saudação, passando um valor de cadeia de caracteres para hello `sendTopicMessage` e qualquer necessária propriedades padrão serão preenchidas por valores padrão.

Olá exemplo a seguir demonstra como toosend cinco mensagens de teste para `MyTopic`. Observe que Olá `messagenumber` varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (isso determinará quais assinaturas recebem-lo):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico. O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma assinatura
As mensagens são recebidas de uma assinatura usando o `receiveSubscriptionMessage` método hello **ServiceBusService** objeto. Por padrão, as mensagens serão excluídas da assinatura Olá conforme elas são de leitura; No entanto, você pode ler (pico) e bloquear a mensagem de saudação sem excluí-lo de assinatura de saudação pelo parâmetro opcional Olá configuração `isPeekLock` muito**true**.

comportamento padrão de saudação de ler e excluir a mensagem de saudação como parte da operação de recebimento é o modelo mais simples de saudação e funciona melhor para cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário no qual a saudação de problemas do consumidor receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Se hello `isPeekLock` parâmetro está definido muito**true**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.
Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa do processo de recebimento chamando **deleteMessage** método e fornecendo o toobe de mensagem excluído como um parâmetro. Olá **deleteMessage** método será marcar a mensagem de saudação como sendo consumida e removê-lo da assinatura de saudação.

Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando `receiveSubscriptionMessage`. Olá exemplo primeiro recebe e exclui uma mensagem de saudação 'LowMessages' de assinatura e, em seguida, recebe uma mensagem de saudação 'HighMessages' assinatura usando `isPeekLock` definir tootrue. Em seguida, exclui hello usando `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método sobre o **ServiceBusService** objeto. Isso causar toounlock do barramento de serviço a mensagem de assinatura do hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada dentro da assinatura, e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e a mensagem de saudação desbloqueia o barramento de serviço automaticamente e o torna disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é feito usando o **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Excluir tópicos e assinaturas
Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente.
Olá exemplo a seguir demonstra como o tópico de saudação toodelete chamado `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Excluir um tópico também excluirá quaisquer assinaturas que são registradas com o tópico de saudação. As assinaturas também podem ser excluídas de forma independente. O exemplo a seguir mostra como toodelete uma assinatura chamada `HighMessages` de saudação `MyTopic` tópico:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.

* Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].
* Referência da API para [SqlFilter][SqlFilter].
* Visite Olá [SDK do Azure para o nó] [ Azure SDK for Node] repositório no GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[criar e implantar um aplicativo de Node. js tooan Site do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
