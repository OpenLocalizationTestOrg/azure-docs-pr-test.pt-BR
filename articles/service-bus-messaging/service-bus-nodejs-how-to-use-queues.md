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
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="676df-103">Como toouse Service Bus filas com Node. js</span><span class="sxs-lookup"><span data-stu-id="676df-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="676df-104">Este artigo descreve como toouse Service Bus filas com Node. js.</span><span class="sxs-lookup"><span data-stu-id="676df-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="676df-105">exemplos de saudação são escritos em JavaScript e usam Olá módulo Azure Node. js.</span><span class="sxs-lookup"><span data-stu-id="676df-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="676df-106">Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**.</span><span class="sxs-lookup"><span data-stu-id="676df-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="676df-107">Para obter mais informações sobre filas, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="676df-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="676df-108">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="676df-108">Create a Node.js application</span></span>
<span data-ttu-id="676df-109">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="676df-109">Create a blank Node.js application.</span></span> <span data-ttu-id="676df-110">Para obter instruções sobre como toocreate um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooan site do Azure][Create and deploy a Node.js application tooan Azure Website], ou [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="676df-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="676df-111">Configurar seu toouse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="676df-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="676df-112">toouse barramento de serviço do Azure, baixe e use Olá pacote do Azure Node. js.</span><span class="sxs-lookup"><span data-stu-id="676df-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="676df-113">Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="676df-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="676df-114">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain</span><span class="sxs-lookup"><span data-stu-id="676df-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="676df-115">Saudação de uso **do Windows PowerShell para Node.js** comando janela toonavigate toohello **c:\\nó\\sbqueues\\WebRole1** pasta na qual você criou seu aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="676df-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="676df-116">Tipo **npm instalar o azure** na janela de comando Olá, que deve resultar no seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="676df-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="676df-117">Você pode executar manualmente Olá **ls** tooverify de comando que um **node_modules** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="676df-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="676df-118">Dentro desse Olá de localizar pasta **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="676df-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="676df-119">Módulo de saudação de importação</span><span class="sxs-lookup"><span data-stu-id="676df-119">Import hello module</span></span>
<span data-ttu-id="676df-120">Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="676df-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="676df-121">Configurar uma conexão do barramento de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="676df-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="676df-122">módulo do Azure Hello lê variável de ambiente Olá `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informações necessárias tooconnect tooService barramento.</span><span class="sxs-lookup"><span data-stu-id="676df-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="676df-123">Se essa variável de ambiente não for definida, você deve especificar as informações de conta de saudação ao chamar `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="676df-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="676df-124">Para obter um exemplo de configuração de variáveis de ambiente Olá em um arquivo de configuração para um serviço de nuvem do Azure, consulte [Node. js serviço de nuvem com o armazenamento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="676df-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="676df-125">Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure] [ Azure portal] para um site do Azure, consulte [aplicativo Web Node.js armazenamento] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="676df-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="676df-126">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="676df-126">Create a queue</span></span>
<span data-ttu-id="676df-127">Olá **ServiceBusService** objeto permite que você toowork com filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="676df-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="676df-128">Olá código a seguir cria um **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="676df-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="676df-129">Adicioná-lo superior de saudação do hello **server.js** arquivo após Olá tooimport da instrução Olá módulo do Azure:</span><span class="sxs-lookup"><span data-stu-id="676df-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="676df-130">Chamando `createQueueIfNotExists` em Olá **ServiceBusService** de objeto, Olá especificado fila será retornada (se houver) ou uma nova fila com o nome especificado da saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="676df-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="676df-131">código a seguir Olá usa `createQueueIfNotExists` toocreate ou conecte-se a fila de toohello denominada `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="676df-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="676df-132">Olá `createServiceBusService` método também oferece suporte a opções adicionais, que permitem a você as configurações de fila de padrão de toooverride como tamanho de fila toolive ou máximo de tempo de mensagem.</span><span class="sxs-lookup"><span data-stu-id="676df-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="676df-133">Olá exemplo a seguir define Olá máximo da fila tamanho too5 GB e um valor de (vida útil TTL) toolive tempo de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="676df-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="676df-134">Filtros</span><span class="sxs-lookup"><span data-stu-id="676df-134">Filters</span></span>
<span data-ttu-id="676df-135">Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="676df-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="676df-136">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="676df-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="676df-137">Depois de fazer seu pré-processamento nas opções de solicitação hello, deve chamar o método hello `next`, passando um retorno de chamada com hello assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="676df-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="676df-138">Em que esse retorno de chamada e depois processamento Olá `returnObject` (hello a resposta do servidor de toohello de solicitação de saudação), retorno de chamada de saudação ou deve chamar `next` se ele existe toocontinue outros filtros de processamento ou simplesmente chamar `finalCallback`, que termina invocação de serviço Hello.</span><span class="sxs-lookup"><span data-stu-id="676df-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="676df-139">Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="676df-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="676df-140">Olá código a seguir cria um `ServiceBusService` objeto que usa Olá `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="676df-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="676df-141">Mensagens tooa fila de envio</span><span class="sxs-lookup"><span data-stu-id="676df-141">Send messages tooa queue</span></span>
<span data-ttu-id="676df-142">toosend uma fila de barramento de serviço tooa mensagens, o aplicativo chama Olá `sendQueueMessage` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="676df-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="676df-143">As mensagens enviadas muito (e recebidas pelo) barramento de serviço filas são **BrokeredMessage** objetos e tem um conjunto de propriedades padrão (como **rótulo** e **TimeToLive**), um dicionário de propriedades específicas do aplicativo personalizadas de toohold usado e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="676df-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="676df-144">Um aplicativo pode definir o corpo de saudação da mensagem de saudação, passando uma cadeia de caracteres como mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="676df-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="676df-145">As propriedades padrão necessárias são preenchidas com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="676df-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="676df-146">Olá exemplo a seguir demonstra como toosend uma fila de toohello de mensagens de teste chamado `myqueue` usando `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="676df-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="676df-147">Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="676df-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="676df-148">cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="676df-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="676df-149">Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="676df-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="676df-150">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="676df-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="676df-151">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="676df-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="676df-152">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="676df-152">Receive messages from a queue</span></span>
<span data-ttu-id="676df-153">As mensagens são recebidas de uma fila usando Olá `receiveQueueMessage` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="676df-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="676df-154">Por padrão, as mensagens serão excluídas da fila de saudação conforme elas são de leitura; No entanto, você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro opcional Olá configuração `isPeekLock` muito**true**.</span><span class="sxs-lookup"><span data-stu-id="676df-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="676df-155">Olá comportamento padrão de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="676df-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="676df-156">toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.</span><span class="sxs-lookup"><span data-stu-id="676df-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="676df-157">Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="676df-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="676df-158">Se hello `isPeekLock` parâmetro está definido muito**true**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="676df-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="676df-159">Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="676df-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="676df-160">Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `deleteMessage` método e fornecendo toobe de mensagem de saudação excluído como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="676df-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="676df-161">Olá `deleteMessage` método marca a mensagem de saudação como sendo consumida e remove da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="676df-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="676df-162">Olá exemplo a seguir demonstra como tooreceive e processar mensagens usando `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="676df-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="676df-163">Olá exemplo primeiro recebe e exclui uma mensagem e, em seguida, recebe uma mensagem usando `isPeekLock` definido muito**true**, em seguida, exclui hello usando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="676df-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="676df-164">Como o aplicativo de toohandle falha e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="676df-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="676df-165">Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="676df-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="676df-166">Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlockMessage` método hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="676df-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="676df-167">Isso causar toounlock do barramento de serviço a mensagem na fila de saudação e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.</span><span class="sxs-lookup"><span data-stu-id="676df-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="676df-168">Também há um tempo limite associado a uma mensagem bloqueada em fila hello e se Olá falha de aplicativo hello tooprocess Olá mensagem antes de tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="676df-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="676df-169">Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `deleteMessage` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="676df-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="676df-170">Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="676df-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="676df-171">Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle.</span><span class="sxs-lookup"><span data-stu-id="676df-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="676df-172">Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="676df-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="676df-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="676df-173">Next steps</span></span>
<span data-ttu-id="676df-174">toolearn mais sobre as filas, consulte Olá recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="676df-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="676df-175">[Filas, tópicos e assinaturas][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="676df-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="676df-176">Repositório do [SDK do Azure para Node][Azure SDK for Node] no GitHub</span><span class="sxs-lookup"><span data-stu-id="676df-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="676df-177">Centro de desenvolvedores do Node. js</span><span class="sxs-lookup"><span data-stu-id="676df-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
