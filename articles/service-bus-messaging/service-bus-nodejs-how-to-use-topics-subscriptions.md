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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="0a7a1-103">Como tooUse Service Bus tópicos e assinaturas com Node. js</span><span class="sxs-lookup"><span data-stu-id="0a7a1-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="0a7a1-104">Este guia descreve como toouse Service Bus tópicos e assinaturas de aplicativos Node. js.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="0a7a1-105">Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **enviando mensagens** tooa tópico **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="0a7a1-106">Para obter mais informações sobre tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="0a7a1-107">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="0a7a1-107">Create a Node.js application</span></span>
<span data-ttu-id="0a7a1-108">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-108">Create a blank Node.js application.</span></span> <span data-ttu-id="0a7a1-109">Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooan Site do Azure], [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell, ou Site da Web com o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="0a7a1-110">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0a7a1-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="0a7a1-111">toouse barramento de serviço, baixe Olá pacote do Azure Node. js.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="0a7a1-112">Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="0a7a1-113">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain</span><span class="sxs-lookup"><span data-stu-id="0a7a1-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="0a7a1-114">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue toohello pasta em que você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="0a7a1-115">Tipo **npm instalar o azure** na janela de comando hello, que deve resultar em Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="0a7a1-116">Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="0a7a1-117">Dentro dessa pasta encontrar o **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess tópicos do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="0a7a1-118">Módulo de saudação de importação</span><span class="sxs-lookup"><span data-stu-id="0a7a1-118">Import hello module</span></span>
<span data-ttu-id="0a7a1-119">Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="0a7a1-120">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="0a7a1-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="0a7a1-121">módulo do Azure Hello lê as variáveis de ambiente Olá `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` para obter informações necessárias tooconnect tooService barramento.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="0a7a1-122">Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="0a7a1-123">Para obter um exemplo de configuração de variáveis de ambiente Olá para um serviço de nuvem do Azure, consulte [Node. js serviço de nuvem com o armazenamento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="0a7a1-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="0a7a1-124">Para obter um exemplo de configuração de variáveis de ambiente Olá para um site do Azure, consulte [aplicativo Web Node.js armazenamento][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="0a7a1-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="0a7a1-125">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="0a7a1-125">Create a topic</span></span>
<span data-ttu-id="0a7a1-126">Olá **ServiceBusService** objeto permite que você toowork com tópicos.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="0a7a1-127">O código a seguir cria um objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="0a7a1-128">Adicioná-lo na parte superior da saudação **server.js** arquivo depois de módulo de saudação do azure Olá instrução tooimport:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="0a7a1-129">Chamando `createTopicIfNotExists` em Olá **ServiceBusService** do objeto, Olá especificado tópico será retornado (se houver), ou será criado um novo tópico com o nome especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="0a7a1-130">código a seguir Olá usa `createTopicIfNotExists` toocreate ou conecte-se toohello tópico chamado `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="0a7a1-131">Olá `createServiceBusService` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações do tópico como vida útil da mensagem ou o tamanho máximo do tópico.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="0a7a1-132">Olá exemplo a seguir define Olá too5GB de tamanho máximo do tópico com um tempo toolive de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="0a7a1-133">Filtros</span><span class="sxs-lookup"><span data-stu-id="0a7a1-133">Filters</span></span>
<span data-ttu-id="0a7a1-134">Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="0a7a1-135">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="0a7a1-136">Depois de executar o pré-processamento nas opções de solicitação hello, Olá chamadas de método `next`, passando um retorno de chamada com hello assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="0a7a1-137">Nesse retorno de chamada e depois processamento Olá `returnObject` (hello a resposta do servidor de toohello de solicitação de saudação), precisa de retorno de chamada hello tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou invocar `finalCallback` Olá de tooend caso contrário, invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="0a7a1-138">Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="0a7a1-139">Olá seguir cria um **ServiceBusService** objeto que usa Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="0a7a1-140">Criar assinaturas</span><span class="sxs-lookup"><span data-stu-id="0a7a1-140">Create subscriptions</span></span>
<span data-ttu-id="0a7a1-141">Assinaturas de tópico também são criadas com hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="0a7a1-142">As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="0a7a1-143">Assinaturas são persistentes e continuarão tooexist até a eles ou hello tópico eles estão associados são excluídos.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="0a7a1-144">Se seu aplicativo contiver lógica toocreate uma assinatura, ele deve primeiro verificar se a assinatura de saudação já existe usando o `getSubscription` método.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="0a7a1-145">Criar uma assinatura com o filtro saudação padrão (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="0a7a1-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="0a7a1-146">Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="0a7a1-147">Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas na fila virtual da assinatura.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="0a7a1-148">Olá, exemplo a seguir cria uma assinatura chamada 'AllMessages' e usa Olá padrão **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="0a7a1-149">Criar assinaturas com os filtros</span><span class="sxs-lookup"><span data-stu-id="0a7a1-149">Create subscriptions with filters</span></span>
<span data-ttu-id="0a7a1-150">Você também pode criar filtros que permitem que você tooscope quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="0a7a1-151">Hello mais flexível o tipo de filtro de assinaturas com suporte é o **SqlFilter**, que implementa um subconjunto do SQL92.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="0a7a1-152">Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="0a7a1-153">Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="0a7a1-154">Filtros podem ser adicionados a assinatura tooa usando Olá `createRule` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="0a7a1-155">Esse método permite que você adicionar nova assinatura existente tooan de filtros.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0a7a1-156">Porque o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou **MatchAll** substituirá os outros filtros que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="0a7a1-157">Você pode remover a regra padrão de saudação usando Olá `deleteRule` método o **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="0a7a1-158">Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `messagenumber` propriedade maior que 3:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="0a7a1-159">Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um `messagenumber` propriedade menor ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="0a7a1-160">Quando uma mensagem agora é enviada muito`MyTopic`, ele sempre será entregue aos destinatários inscrito toohello `AllMessages` assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello `HighMessages` e `LowMessages` assinaturas de tópico (dependendo de conteúdo da mensagem de saudação).</span><span class="sxs-lookup"><span data-stu-id="0a7a1-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="0a7a1-161">Como as mensagens de toosend tooa tópico</span><span class="sxs-lookup"><span data-stu-id="0a7a1-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="0a7a1-162">toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar o `sendTopicMessage` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="0a7a1-163">As mensagens enviadas são tópicos do barramento tooService **BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="0a7a1-164">**BrokeredMessage** objetos têm um conjunto de propriedades padrão (como `Label` e `TimeToLive`), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="0a7a1-165">Um aplicativo pode definir o corpo de saudação da mensagem de saudação, passando um valor de cadeia de caracteres para hello `sendTopicMessage` e qualquer necessária propriedades padrão serão preenchidas por valores padrão.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="0a7a1-166">Olá exemplo a seguir demonstra como toosend cinco mensagens de teste para `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="0a7a1-167">Observe que Olá `messagenumber` varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (isso determinará quais assinaturas recebem-lo):</span><span class="sxs-lookup"><span data-stu-id="0a7a1-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="0a7a1-168">Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="0a7a1-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="0a7a1-169">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="0a7a1-170">Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="0a7a1-171">O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="0a7a1-172">Receber mensagens de uma assinatura</span><span class="sxs-lookup"><span data-stu-id="0a7a1-172">Receive messages from a subscription</span></span>
<span data-ttu-id="0a7a1-173">As mensagens são recebidas de uma assinatura usando o `receiveSubscriptionMessage` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="0a7a1-174">Por padrão, as mensagens serão excluídas da assinatura Olá conforme elas são de leitura; No entanto, você pode ler (pico) e bloquear a mensagem de saudação sem excluí-lo de assinatura de saudação pelo parâmetro opcional Olá configuração `isPeekLock` muito**true**.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="0a7a1-175">comportamento padrão de saudação de ler e excluir a mensagem de saudação como parte da operação de recebimento é o modelo mais simples de saudação e funciona melhor para cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="0a7a1-176">toounderstand isso, considere um cenário no qual a saudação de problemas do consumidor receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="0a7a1-177">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="0a7a1-178">Se hello `isPeekLock` parâmetro está definido muito**true**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="0a7a1-179">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="0a7a1-180">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa do processo de recebimento chamando **deleteMessage** método e fornecendo o toobe de mensagem excluído como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="0a7a1-181">Olá **deleteMessage** método será marcar a mensagem de saudação como sendo consumida e removê-lo da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="0a7a1-182">Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="0a7a1-183">Olá exemplo primeiro recebe e exclui uma mensagem de saudação 'LowMessages' de assinatura e, em seguida, recebe uma mensagem de saudação 'HighMessages' assinatura usando `isPeekLock` definir tootrue.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="0a7a1-184">Em seguida, exclui hello usando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="0a7a1-185">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="0a7a1-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="0a7a1-186">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="0a7a1-187">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método sobre o **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="0a7a1-188">Isso causar toounlock do barramento de serviço a mensagem de assinatura do hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="0a7a1-189">Também há um tempo limite associado a uma mensagem bloqueada dentro da assinatura, e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e a mensagem de saudação desbloqueia o barramento de serviço automaticamente e o torna disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="0a7a1-190">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="0a7a1-191">Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="0a7a1-192">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="0a7a1-193">Isso geralmente é feito usando o **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="0a7a1-194">Excluir tópicos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="0a7a1-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="0a7a1-195">Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="0a7a1-196">Olá exemplo a seguir demonstra como o tópico de saudação toodelete chamado `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="0a7a1-197">Excluir um tópico também excluirá quaisquer assinaturas que são registradas com o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="0a7a1-198">As assinaturas também podem ser excluídas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="0a7a1-199">O exemplo a seguir mostra como toodelete uma assinatura chamada `HighMessages` de saudação `MyTopic` tópico:</span><span class="sxs-lookup"><span data-stu-id="0a7a1-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="0a7a1-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a7a1-200">Next Steps</span></span>
<span data-ttu-id="0a7a1-201">Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="0a7a1-202">Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="0a7a1-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="0a7a1-203">Referência da API para [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="0a7a1-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="0a7a1-204">Visite Olá [SDK do Azure para o nó] [ Azure SDK for Node] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a7a1-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[criar e implantar um aplicativo de Node. js tooan Site do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
