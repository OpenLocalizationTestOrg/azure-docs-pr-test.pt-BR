---
title: "Como usar as filas de Barramento de Serviço no Node.js | Microsoft Docs"
description: "Aprenda a usar as filas do Barramento de Serviço no Azure a partir de um aplicativo Node.js."
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
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="cc147-103">Como usar filas do Barramento de Serviço com Node.js</span><span class="sxs-lookup"><span data-stu-id="cc147-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="cc147-104">Este artigo descreve como usar as filas do Barramento de Serviço com Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc147-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="cc147-105">As amostras são escritas em JavaScript e usam o módulo Node.js do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="cc147-106">Os cenários cobertos incluem **criar filas**, **enviar e receber mensagens** e **excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="cc147-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="cc147-107">Para obter mais informações sobre filas, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="cc147-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="cc147-108">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="cc147-108">Create a Node.js application</span></span>
<span data-ttu-id="cc147-109">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="cc147-109">Create a blank Node.js application.</span></span> <span data-ttu-id="cc147-110">Para obter instruções sobre como criar um aplicativo Node.js, confira [Criar e implantar um aplicativo do Node.js em um site da Web do Azure][Create and deploy a Node.js application to an Azure Website] ou [Serviço de Nuvem do Node.js][Node.js Cloud Service] usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc147-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="cc147-111">Configurar seu aplicativo para usar o Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="cc147-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="cc147-112">Para usar o Barramento de Serviço do Azure, baixe e use o pacote do Azure Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc147-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="cc147-113">Este pacote inclui um conjunto de bibliotecas que se comunicam com os serviços REST do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="cc147-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="cc147-114">Usar o NPM (gerenciador de pacotes de nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="cc147-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="cc147-115">Use a janela de comando **Windows PowerShell para Node.js** para navegar até a pasta **c:\\node\\sbqueues\\WebRole1** na qual você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cc147-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="cc147-116">Digite **npm install azure** na janela Comando, o que deve resultar em uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="cc147-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

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
3. <span data-ttu-id="cc147-117">Você pode executar manualmente o comando **ls** para verificar se uma pasta **node_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="cc147-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="cc147-118">Dentro dessa pasta, você encontrará o pacote **azure**, que contém as bibliotecas necessárias para acessar as filas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="cc147-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="cc147-119">Importar o módulo</span><span class="sxs-lookup"><span data-stu-id="cc147-119">Import the module</span></span>
<span data-ttu-id="cc147-120">Usando o Bloco de Notas ou outro editor de texto, adicione o seguinte ao início do arquivo **server.js** do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="cc147-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="cc147-121">Configurar uma conexão do barramento de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="cc147-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="cc147-122">O módulo do Azure lê a variável de ambiente `AZURE_SERVICEBUS_CONNECTION_STRING` para obter as informações necessárias para se conectar ao Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="cc147-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="cc147-123">Se essa variável de ambiente não estiver definida, você deverá especificar as informações da conta chamando `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="cc147-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="cc147-124">Para obter um exemplo de como definir as variáveis de ambiente em um arquivo de configuração para um Serviço de Nuvem do Azure, confira [Serviço de Nuvem do Node.js com Armazenamento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="cc147-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="cc147-125">Para ver um exemplo de como definir variáveis de ambiente no [Portal do Azure][Azure portal] para um Site do Azure, veja [Aplicativo Web do Node.js com Armazenamento][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="cc147-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="cc147-126">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="cc147-126">Create a queue</span></span>
<span data-ttu-id="cc147-127">O objeto **ServiceBusService** permite que você trabalhe com filas de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="cc147-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="cc147-128">O código a seguir cria um objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="cc147-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="cc147-129">Adicione-o próximo ao início do arquivo **server.js** , após a instrução de importação do módulo Azure:</span><span class="sxs-lookup"><span data-stu-id="cc147-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="cc147-130">Ao chamar `createQueueIfNotExists` no objeto **ServiceBusService**, a fila especificada (se houver) é retornada ou uma nova fila com o nome especificado é criada.</span><span class="sxs-lookup"><span data-stu-id="cc147-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="cc147-131">O código a seguir usa `createQueueIfNotExists` para criar ou conectar-se à fila denominada `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="cc147-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="cc147-132">O método `createServiceBusService` também dá suporte para opções adicionais, que permitem a substituição de configurações padrão da fila, como a vida útil da mensagem ou o tamanho máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="cc147-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="cc147-133">O exemplo a seguir define o tamanho máximo da fila como 5 GB e a vida útil (TTL) como um minuto:</span><span class="sxs-lookup"><span data-stu-id="cc147-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="cc147-134">Filtros</span><span class="sxs-lookup"><span data-stu-id="cc147-134">Filters</span></span>
<span data-ttu-id="cc147-135">É possível aplicar operações de filtragem opcionais às operações executadas usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="cc147-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="cc147-136">As operações de filtragem podem incluir registro em log, repetição automática, etc. Filtros são objetos que implementam um método com a assinatura:</span><span class="sxs-lookup"><span data-stu-id="cc147-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="cc147-137">Após fazer seu pré-processamento nas opções de solicitação, o método precisará chamar `next`, passando um retorno de chamada com a assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc147-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="cc147-138">Nesse retorno de chamada, e após processar o `returnObject` (a resposta da solicitação ao servidor), o retorno de chamada precisará invocar `next`, se ele existir, para continuar processando outros filtros ou simplesmente invocar `finalCallback`, para terminar a invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="cc147-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="cc147-139">Dois filtros que implementam a lógica de repetição são incluídos com o Azure SDK para Node.js, `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="cc147-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="cc147-140">O código a seguir cria um objeto `ServiceBusService` que usa o `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="cc147-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="cc147-141">Enviar mensagens a uma fila</span><span class="sxs-lookup"><span data-stu-id="cc147-141">Send messages to a queue</span></span>
<span data-ttu-id="cc147-142">Para enviar uma mensagem para uma fila do Barramento de Serviço, seu aplicativo chamará o método `sendQueueMessage` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="cc147-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="cc147-143">Mensagens enviadas para (e recebidas de) as filas do Barramento de Serviço são objetos **BrokeredMessage** e têm um conjunto de propriedades padrão (como **Label** e **TimeToLive**), um dicionário que é usado para manter propriedades personalizadas específicas ao aplicativo e um corpo de dados arbitrários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc147-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="cc147-144">Um aplicativo pode definir o corpo da mensagem passando uma cadeia de caracteres como a mensagem.</span><span class="sxs-lookup"><span data-stu-id="cc147-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="cc147-145">As propriedades padrão necessárias são preenchidas com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="cc147-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="cc147-146">O exemplo a seguir demonstra como enviar uma mensagem de teste à fila chamada `myqueue` usando `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="cc147-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="cc147-147">As filas do Barramento de Serviço dão suporte ao tamanho máximo de mensagem de 256 KB na [camada Standard](service-bus-premium-messaging.md) e 1 MB na [camada Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="cc147-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="cc147-148">O cabeçalho, que inclui as propriedades de aplicativo padrão e personalizadas, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="cc147-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="cc147-149">Não há nenhum limite no número de mensagens mantidas em uma fila mas há uma capacidade do tamanho total das mensagens mantidas por uma fila.</span><span class="sxs-lookup"><span data-stu-id="cc147-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="cc147-150">O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="cc147-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="cc147-151">Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).</span><span class="sxs-lookup"><span data-stu-id="cc147-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="cc147-152">Receber mensagens de uma fila</span><span class="sxs-lookup"><span data-stu-id="cc147-152">Receive messages from a queue</span></span>
<span data-ttu-id="cc147-153">As mensagens são recebidas de uma fila usando o método `receiveQueueMessage` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="cc147-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="cc147-154">Por padrão, as mensagens são excluídas da fila à medida que são lidas; no entanto, você pode ler (pico) e bloquear a mensagem sem excluí-la da fila configurando o parâmetro opcional `isPeekLock` como **true**.</span><span class="sxs-lookup"><span data-stu-id="cc147-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="cc147-155">O comportamento padrão da leitura e da exclusão da mensagem como parte da operação de recebimento é o modelo mais simples e funciona melhor em cenários nos quais um aplicativo possa tolerar o não processamento de uma mensagem em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="cc147-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="cc147-156">Para compreender isso, considere um cenário no qual o consumidor emite a solicitação de recebimento e então falha antes de processá-la.</span><span class="sxs-lookup"><span data-stu-id="cc147-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="cc147-157">Como o Barramento de Serviço terá marcado a mensagem como sendo consumida, quando o aplicativo for reiniciado e começar a consumir mensagens novamente, ele terá perdido a mensagem que foi consumida antes da falha.</span><span class="sxs-lookup"><span data-stu-id="cc147-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="cc147-158">Se o parâmetro `isPeekLock` estiver definido como **true**, o processo de recebimento se torna uma operação de duas etapas, o que torna possível o suporte a aplicativos que não toleram mensagens ausentes.</span><span class="sxs-lookup"><span data-stu-id="cc147-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="cc147-159">Quando o Barramento de Serviço recebe uma solicitação, ele encontra a próxima mensagem a ser consumida, a bloqueia para evitar que outros clientes a recebam e a retorna para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc147-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="cc147-160">Depois que o aplicativo termina de processar a mensagem (ou a armazena de forma segura para um processamento futuro), ele conclui o segundo estágio do processo de recebimento, chamando o método `deleteMessage` e fornecendo a mensagem a ser excluída como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="cc147-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="cc147-161">O método `deleteMessage` marcará a mensagem como sendo consumida e a removerá da assinatura.</span><span class="sxs-lookup"><span data-stu-id="cc147-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="cc147-162">O exemplo a seguir demonstra como receber e processar mensagens usando `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="cc147-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="cc147-163">Primeiro, o exemplo recebe e exclui uma mensagem, em seguida recebe a mensagem usando `isPeekLock` definido como **true** e, então, exclui a mensagem usando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="cc147-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="cc147-164">Como tratar falhas do aplicativo e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="cc147-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="cc147-165">O Barramento de Serviço proporciona funcionalidade para ajudá-lo a se recuperar normalmente dos erros no seu aplicativo ou das dificuldades no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="cc147-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="cc147-166">Se um aplicativo receptor não puder processar a mensagem por algum motivo, ele chamará o método `unlockMessage` no objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="cc147-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="cc147-167">Isso fará com que o Service Bus desbloqueie a mensagem na fila e disponibilize-a para que ela possa ser recebida novamente pelo mesmo aplicativo de consumo ou por outro.</span><span class="sxs-lookup"><span data-stu-id="cc147-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="cc147-168">Também há um tempo limite associado a uma mensagem bloqueada na fila e, se o aplicativo não conseguir processar a mensagem antes da expiração do tempo limite do bloqueio (por exemplo, em caso de falha do aplicativo), o Service Bus desbloqueará a mensagem automaticamente e a disponibilizará para ser recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="cc147-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="cc147-169">Caso o aplicativo falhe após o processamento da mensagem, mas antes que o método `deleteMessage` seja chamado, a mensagem será fornecida novamente ao aplicativo quando ele for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="cc147-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="cc147-170">Isso é frequentemente chamado de *Processamento de pelo menos uma vez*, ou seja, cada mensagem será processada pelo menos uma vez mas, em algumas situações, a mesma mensagem poderá ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="cc147-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="cc147-171">Se o cenário não tolerar o processamento duplicado, os desenvolvedores de aplicativos deverão adicionar lógica extra ao aplicativo para tratar a entrega de mensagem duplicada.</span><span class="sxs-lookup"><span data-stu-id="cc147-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="cc147-172">Isso geralmente é obtido com a propriedade **MessageId** da mensagem, que permanecerá constante nas tentativas da entrega.</span><span class="sxs-lookup"><span data-stu-id="cc147-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc147-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc147-173">Next steps</span></span>
<span data-ttu-id="cc147-174">Para saber mais sobre filas, veja os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="cc147-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="cc147-175">[Filas, tópicos e assinaturas][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="cc147-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="cc147-176">Repositório do [SDK do Azure para Node][Azure SDK for Node] no GitHub</span><span class="sxs-lookup"><span data-stu-id="cc147-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="cc147-177">Centro de desenvolvedores do Node. js</span><span class="sxs-lookup"><span data-stu-id="cc147-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
