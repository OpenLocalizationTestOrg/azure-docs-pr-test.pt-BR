---
title: "Como usar tópicos e assinaturas do Barramento de Serviço do Azure com o Node.js | Microsoft Docs"
description: "Aprenda a usar assinaturas e tópicos do Barramento de Serviço no Azure por meio de um aplicativo Node.js."
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
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="21957-103">Como usar tópicos e assinaturas do Barramento de Serviço com Node.js</span><span class="sxs-lookup"><span data-stu-id="21957-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="21957-104">Este guia descreve como usar tópicos do Barramento de Serviço e assinaturas de aplicativos Node.js.</span><span class="sxs-lookup"><span data-stu-id="21957-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="21957-105">Os cenários abordados incluem a **criação de tópicos e assinaturas**, a **criação de filtros de assinatura**, o **envio de mensagens para um tópico**, o **recebimento de mensagens de uma assinatura** e a **exclusão de tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="21957-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="21957-106">Para saber mais sobre tópicos e assinaturas, confira a seção [Próximas etapas](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="21957-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="21957-107">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="21957-107">Create a Node.js application</span></span>
<span data-ttu-id="21957-108">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="21957-108">Create a blank Node.js application.</span></span> <span data-ttu-id="21957-109">Para obter instruções sobre como criar um aplicativo Node.js, confira [Criar e implantar um aplicativo Node.js em um site da Web do Azure], [Serviço de Nuvem do Node.js][Node.js Cloud Service] usando o Windows PowerShell ou Site com o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="21957-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="21957-110">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="21957-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="21957-111">Para usar o Barramento de Serviço, baixe o pacote do Node.js do Azure.</span><span class="sxs-lookup"><span data-stu-id="21957-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="21957-112">Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="21957-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="21957-113">Usar o NPM (gerenciador de pacotes de nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="21957-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="21957-114">Use uma interface de linha de comando, como **PowerShell** (Windows), **Terminal** (Mac,) ou **Bash** (Unix), e navegue até a pasta onde você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="21957-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="21957-115">Digite **npm install azure** na janela de comando, que deve resultar na seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="21957-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

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
3. <span data-ttu-id="21957-116">Você pode executar manualmente o comando **ls** para verificar se uma pasta **node\_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="21957-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="21957-117">Dentro dessa pasta, você encontrará o pacote **azure**, que contém as bibliotecas necessárias para acessar os tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="21957-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="21957-118">Importar o módulo</span><span class="sxs-lookup"><span data-stu-id="21957-118">Import the module</span></span>
<span data-ttu-id="21957-119">Usando o Bloco de Notas ou outro editor de texto, adicione o seguinte ao início do arquivo **server.js** do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="21957-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="21957-120">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="21957-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="21957-121">O módulo do Azure lê a variável de ambiente `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` para obter as informações necessárias para se conectar ao Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="21957-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="21957-122">Se essas variáveis de ambiente não estiverem definidas, você deverá especificar as informações da conta ao chamar `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="21957-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="21957-123">Para obter um exemplo de como definir as variáveis de ambiente para um serviço de nuvem do Azure, confira [Serviço de nuvem do Node.js com armazenamento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="21957-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="21957-124">Para ver um exemplo de como definir variáveis de ambiente para um Site do Azure, veja [Aplicativo Web do Node.js com Armazenamento][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="21957-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="21957-125">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="21957-125">Create a topic</span></span>
<span data-ttu-id="21957-126">O objeto **ServiceBusService** permite que você trabalhe com tópicos.</span><span class="sxs-lookup"><span data-stu-id="21957-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="21957-127">O código a seguir cria um objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="21957-128">Adicione-o próximo ao início do arquivo **server.js** , após a instrução de importação do módulo Azure:</span><span class="sxs-lookup"><span data-stu-id="21957-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="21957-129">Ao chamar `createTopicIfNotExists` no objeto **ServiceBusService**, o tópico especificado (se houver) será retornado ou um novo tópico com o nome especificado será criado.</span><span class="sxs-lookup"><span data-stu-id="21957-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="21957-130">O código a seguir usa `createTopicIfNotExists` para criar ou conectar-se ao tópico denominado `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="21957-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="21957-131">O método `createServiceBusService` também dá suporte a opções adicionais, que permitem substituir configurações padrão do tópico, como a vida útil da mensagem ou o tamanho máximo do tópico.</span><span class="sxs-lookup"><span data-stu-id="21957-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="21957-132">O exemplo a seguir define o tamanho máximo do tópico como 5 GB com uma vida útil de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="21957-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="21957-133">Filtros</span><span class="sxs-lookup"><span data-stu-id="21957-133">Filters</span></span>
<span data-ttu-id="21957-134">É possível aplicar operações de filtragem opcionais às operações executadas usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="21957-135">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com a assinatura:</span><span class="sxs-lookup"><span data-stu-id="21957-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="21957-136">Após fazer o pré-processamento nas opções de solicitação, o método precisará chamar `next`, passando um retorno de chamada com a assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="21957-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="21957-137">Nesse retorno de chamada, e depois de processar o `returnObject` (a resposta da solicitação ao servidor), o retorno de chamada precisará invocar “next”, se ele existir, para continuar processando outros filtros ou simplesmente invocar `finalCallback` para terminar a invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="21957-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="21957-138">Dois filtros que implementam a lógica de repetição estão incluídos no SDK do Azure para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="21957-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="21957-139">O seguinte código cria um objeto **ServiceBusService** que usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="21957-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="21957-140">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="21957-140">Create subscriptions</span></span>
<span data-ttu-id="21957-141">As assinaturas do tópico também são criadas com o objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="21957-142">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de mensagens entregues à fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="21957-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="21957-143">As assinaturas são persistentes e continuarão existindo até que elas ou o tópico ao qual estão associadas sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="21957-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="21957-144">Se seu aplicativo contiver a lógica para criar uma assinatura, ele deve primeiro verificar se a assinatura já existe usando o método `getSubscription`.</span><span class="sxs-lookup"><span data-stu-id="21957-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="21957-145">Criar uma assinatura com o filtro padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="21957-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="21957-146">O filtro **MatchAll** será o padrão usado se nenhum filtro for especificado quando uma nova assinatura for criada.</span><span class="sxs-lookup"><span data-stu-id="21957-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="21957-147">Quando o filtro **MatchAll** é usado, todas as mensagens publicadas no tópico são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="21957-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="21957-148">O exemplo a seguir cria uma assinatura denominada “AllMessages” e usa o filtro padrão **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="21957-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="21957-149">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="21957-149">Create subscriptions with filters</span></span>
<span data-ttu-id="21957-150">Você também pode configurar filtros que permitem atribuir um escopo a quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica do tópico.</span><span class="sxs-lookup"><span data-stu-id="21957-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="21957-151">O tipo de filtro mais flexível compatível com as assinaturas é o **SqlFilter**, que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="21957-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="21957-152">Os filtros SQL operam nas propriedades das mensagens que são publicadas no tópico.</span><span class="sxs-lookup"><span data-stu-id="21957-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="21957-153">Para obter mais detalhes sobre as expressões que podem ser usadas com um filtro SQL, examine a sintaxe [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="21957-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="21957-154">Os filtros podem ser adicionados a uma assinatura usando o método `createRule` do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="21957-155">Este método permite que você adicione novos filtros a uma assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="21957-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="21957-156">Como o filtro padrão é aplicado automaticamente em todas as assinaturas novas, você deve primeiro remover o filtro padrão, senão o filtro **MatchAll** substituirá todos os outros filtros que você possa especificar.</span><span class="sxs-lookup"><span data-stu-id="21957-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="21957-157">Você pode remover a regra padrão usando o método `deleteRule` do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="21957-158">O exemplo a seguir cria uma assinatura denominada `HighMessages` com um **SqlFilter** que seleciona apenas as mensagens que tenham uma propriedade personalizada `messagenumber` maior que 3:</span><span class="sxs-lookup"><span data-stu-id="21957-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="21957-159">Da mesma forma, o seguinte exemplo cria uma assinatura denominada `LowMessages` com um **SqlFilter** que seleciona apenas mensagens que têm uma propriedade `messagenumber` menor ou igual a 3:</span><span class="sxs-lookup"><span data-stu-id="21957-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

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

<span data-ttu-id="21957-160">Quando uma mensagem é agora enviada para `MyTopic`, ela sempre será entregue aos destinatários inscritos na assinatura do tópico `AllMessages` e entregue de forma seletiva aos destinatários inscritos nas assinaturas do tópico `HighMessages` e `LowMessages` (dependendo do conteúdo da mensagem).</span><span class="sxs-lookup"><span data-stu-id="21957-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="21957-161">Como enviar mensagens a um tópico</span><span class="sxs-lookup"><span data-stu-id="21957-161">How to send messages to a topic</span></span>
<span data-ttu-id="21957-162">Para enviar uma mensagem a um tópico do Barramento de Serviço, seu aplicativo deve usar o método `sendTopicMessage` do objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="21957-163">As mensagens enviadas aos tópicos do Barramento de Serviço são objetos **BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="21957-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="21957-164">Os objetos **BrokeredMessage** têm um conjunto de propriedades padrão (como `Label` e `TimeToLive`), um dicionário usado para manter as propriedades personalizadas específicas do aplicativo e um corpo dos dados da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="21957-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="21957-165">Um aplicativo pode definir o corpo da mensagem transmitindo um valor da cadeia ao `sendTopicMessage` e todas as propriedades padrão exigidas serão preenchidas por valores padrão.</span><span class="sxs-lookup"><span data-stu-id="21957-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="21957-166">O exemplo a seguir demonstra como enviar cinco mensagens de teste para `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="21957-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="21957-167">Observe que o valor da propriedade `messagenumber` de cada mensagem varia de acordo com a iteração do loop (isso determinará qual assinatura o receberá):</span><span class="sxs-lookup"><span data-stu-id="21957-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="21957-168">Os tópicos do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="21957-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="21957-169">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="21957-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="21957-170">Não há nenhum limite no número de mensagens mantidas em um tópico, mas há uma capacidade do tamanho total das mensagens mantidas por um tópico.</span><span class="sxs-lookup"><span data-stu-id="21957-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="21957-171">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="21957-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="21957-172">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="21957-172">Receive messages from a subscription</span></span>
<span data-ttu-id="21957-173">As mensagens são recebidas de uma assinatura usando o método `receiveSubscriptionMessage` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="21957-174">Por padrão, as mensagens são excluídas da assinatura à medida que são lidas. No entanto, você pode ler (espiar) e bloquear a mensagem sem excluí-la da assinatura, definindo o parâmetro opcional `isPeekLock` como **true**.</span><span class="sxs-lookup"><span data-stu-id="21957-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="21957-175">O comportamento padrão da leitura e da exclusão da mensagem como parte da operação de recebimento é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo possa tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="21957-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="21957-176">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="21957-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="21957-177">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="21957-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="21957-178">Se o parâmetro `isPeekLock` estiver definido como **true**, o processo de recebimento se torna uma operação de duas etapas, o que torna possível o suporte a aplicativos que não toleram mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="21957-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="21957-179">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21957-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="21957-180">Depois que o aplicativo termina de processar a mensagem (ou a armazena de forma segura para um processamento futuro), ele conclui o segundo estágio do processo de recebimento, chamando o método **deleteMessage** e fornecendo a mensagem a ser excluída como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="21957-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="21957-181">O método **deleteMessage** marcará a mensagem como tendo sido consumida e a removerá da assinatura.</span><span class="sxs-lookup"><span data-stu-id="21957-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="21957-182">O exemplo a seguir demonstra como as mensagens podem ser recebidas e processadas usando o modo `receiveSubscriptionMessage` padrão.</span><span class="sxs-lookup"><span data-stu-id="21957-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="21957-183">O primeiro exemplo recebe e exclui uma mensagem da assinatura “LowMessages” e recebe uma mensagem da assinatura “HighMessages” usando `isPeekLock` definido como true.</span><span class="sxs-lookup"><span data-stu-id="21957-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="21957-184">Em seguida, ele exclui a mensagem usando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="21957-184">It then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="21957-185">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="21957-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="21957-186">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="21957-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="21957-187">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele chamará o método `unlockMessage` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="21957-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="21957-188">Isso fará com que o Barramento de Serviço desbloqueie a mensagem na assinatura e disponibilize-a para ser recebida novamente, pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="21957-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="21957-189">Também há um tempo limite associado a uma mensagem bloqueada na assinatura e, se houver falha no processamento da mensagem pelo aplicativo antes da expiração do tempo limite de bloqueio (por exemplo, se o aplicativo travar), o Barramento de Serviço desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="21957-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="21957-190">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método `deleteMessage` seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="21957-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="21957-191">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="21957-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="21957-192">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="21957-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="21957-193">Isso geralmente é obtido com a propriedade **MessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="21957-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="21957-194">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="21957-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="21957-195">Os tópicos e as assinaturas são persistentes e devem ser explicitamente excluídos por meio do [Portal do Azure][Azure portal] ou de forma programática.</span><span class="sxs-lookup"><span data-stu-id="21957-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="21957-196">O exemplo a seguir demonstra como excluir o tópico denominado `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="21957-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="21957-197">A exclusão de um tópico também excluirá todas as assinaturas registradas com o tópico.</span><span class="sxs-lookup"><span data-stu-id="21957-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="21957-198">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="21957-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="21957-199">O código a seguir demonstra como excluir uma assinatura chamada `HighMessages` do tópico `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="21957-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="21957-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21957-200">Next Steps</span></span>
<span data-ttu-id="21957-201">Agora que você já sabe os princípios dos tópicos do Barramento de Serviço, acesse estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="21957-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="21957-202">Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="21957-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="21957-203">Referência da API para [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="21957-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="21957-204">Visite o repositório [SDK do Azure para o nó][Azure SDK for Node] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="21957-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Criar e implantar um aplicativo Node.js em um site da Web do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
