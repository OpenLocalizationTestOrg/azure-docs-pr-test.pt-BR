---
title: Como usar o Armazenamento de Filas do Node.js | Microsoft Docs
description: "Saiba como usar o serviço Fila do Azure para criar e excluir filas, bem como para inserir, obter e excluir mensagens. Amostras escritas em Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 15c1d3cb6eac8fc14837277c4a4275dea91701cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="288fa-104">Como usar o Armazenamento de Fila do Node.js</span><span class="sxs-lookup"><span data-stu-id="288fa-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="288fa-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="288fa-105">Overview</span></span>
<span data-ttu-id="288fa-106">Este guia mostra como executar cenários comuns usando o serviço Fila do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="288fa-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="288fa-107">As amostras são gravadas usando a API do Node.js.</span><span class="sxs-lookup"><span data-stu-id="288fa-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="288fa-108">Os cenários abrangidos incluem **inserir**, **exibir**, **obter** e **excluir** mensagens da fila, bem como **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="288fa-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="288fa-109">Criar um aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="288fa-109">Create a Node.js Application</span></span>
<span data-ttu-id="288fa-110">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="288fa-110">Create a blank Node.js application.</span></span> <span data-ttu-id="288fa-111">Para obter instruções sobre como criar um aplicativo do Node.js, confira [Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [Criar e implantar um aplicativo Node.js para um Serviço de Nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) usando o Windows PowerShell ou [Criar e implantar um aplicativo Web Node.js no Azure usando a Matriz da Web](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="288fa-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="288fa-112">Configurar seu aplicativo para acessar o armazenamento</span><span class="sxs-lookup"><span data-stu-id="288fa-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="288fa-113">Para usar o armazenamento do Azure, você precisa do SDK de Armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas convenientes que se comunicam com os serviços REST do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="288fa-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="288fa-114">Usar o NPM (gerenciador de pacotes de nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="288fa-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="288fa-115">Use uma interface de linha de comando, como **PowerShell** (Windows), **Terminal** (Mac,) ou **Bash** (Unix), e navegue até a pasta onde você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="288fa-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="288fa-116">Digite **npm install azure-storage** na janela de comando.</span><span class="sxs-lookup"><span data-stu-id="288fa-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="288fa-117">A saída do comando é semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="288fa-117">Output from the command is similar to the following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="288fa-118">Você pode executar manualmente o comando **ls** para verificar se uma pasta **node\_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="288fa-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="288fa-119">Dentro dessa pasta, você encontrará o pacote **azure-storage** que contém as bibliotecas necessárias para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="288fa-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="288fa-120">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="288fa-120">Import the package</span></span>
<span data-ttu-id="288fa-121">Usando o Bloco de Notas ou outro editor de texto, adicione o seguinte à parte superior do arquivo **server.js** do aplicativo no qual você pretende usar o armazenamento:</span><span class="sxs-lookup"><span data-stu-id="288fa-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="288fa-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="288fa-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="288fa-123">O módulo do Azure lerá as variáveis de ambiente AZURE\_STORAGE\_ACCOUNT e AZURE\_STORAGE\_ACCESS\_KEY ou AZURE\_STORAGE\_CONNECTION\_STRING para obter as informações necessárias para se conectar à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="288fa-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="288fa-124">Se essas variáveis de ambiente não estiverem definidas, você deverá especificar as informações da conta ao chamar **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="288fa-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="288fa-125">Para obter um exemplo de como definir as variáveis de ambiente no [Portal do Azure](https://portal.azure.com) para um Site do Azure, consulte [Aplicativo Web Node.js com o Serviço Tabela do Azure].</span><span class="sxs-lookup"><span data-stu-id="288fa-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="288fa-126">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="288fa-126">How To: Create a Queue</span></span>
<span data-ttu-id="288fa-127">O código a seguir cria um objeto **QueueService** , permitindo que você trabalhe com filas.</span><span class="sxs-lookup"><span data-stu-id="288fa-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="288fa-128">Use o método **createQueueIfNotExists** , que retorna a fila especificada, se já existente, ou cria uma nova fila com o nome especificado se esse nome ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="288fa-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="288fa-129">Se a fila for criada, `result.created` é true.</span><span class="sxs-lookup"><span data-stu-id="288fa-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="288fa-130">Se a fila existir, `result.created` é false.</span><span class="sxs-lookup"><span data-stu-id="288fa-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="288fa-131">Filtros</span><span class="sxs-lookup"><span data-stu-id="288fa-131">Filters</span></span>
<span data-ttu-id="288fa-132">É possível aplicar operações de filtragem opcionais às operações executadas usando **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="288fa-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="288fa-133">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com a assinatura:</span><span class="sxs-lookup"><span data-stu-id="288fa-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="288fa-134">Após fazer seu pré-processamento nas opções de solicitação, o método precisará chamar "next", passando um retorno de chamada com a assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="288fa-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="288fa-135">Nesse retorno de chamada, e após processar o returnObject (a resposta da solicitação ao servidor), o retorno de chamada precisará invocar avançar, se ele existir, para continuar processando outros filtros ou simplesmente invocar finalCallback para terminar a invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="288fa-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="288fa-136">Dois filtros que implementam a lógica de repetição estão incluídos no SDK do Azure para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="288fa-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="288fa-137">O seguinte código cria um objeto **QueueService** que usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="288fa-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="288fa-138">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="288fa-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="288fa-139">Para inserir uma mensagem em uma fila, use o método **createMessage** para criar uma nova mensagem e adicione-a à fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="288fa-140">Como: espiar a próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="288fa-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="288fa-141">Você pode inspecionar a mensagem na frente de uma fila sem removê-la da fila chamando o método **peekMessages** .</span><span class="sxs-lookup"><span data-stu-id="288fa-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="288fa-142">Por padrão, **peekMessages** inspeciona uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="288fa-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="288fa-143">O `result` contém a mensagem.</span><span class="sxs-lookup"><span data-stu-id="288fa-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="288fa-144">Usar **peekMessages** quando não existirem mensagens na fila não retornará um erro; no entanto, nenhuma mensagem será retornada.</span><span class="sxs-lookup"><span data-stu-id="288fa-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="288fa-145">Como: remover a próxima mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="288fa-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="288fa-146">O processamento de uma mensagem é um processo de duas fases:</span><span class="sxs-lookup"><span data-stu-id="288fa-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="288fa-147">Remover a mensagem.</span><span class="sxs-lookup"><span data-stu-id="288fa-147">Dequeue the message.</span></span>
2. <span data-ttu-id="288fa-148">Excluir a mensagem.</span><span class="sxs-lookup"><span data-stu-id="288fa-148">Delete the message.</span></span>

<span data-ttu-id="288fa-149">Para remover uma mensagem da fila, use **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="288fa-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="288fa-150">Isso torna as mensagens invisíveis na fila, de forma que nenhum outro cliente possa processá-las.</span><span class="sxs-lookup"><span data-stu-id="288fa-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="288fa-151">Depois que seu aplicativo tiver processado uma mensagem, chame **deleteMessage** para excluí-la da fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="288fa-152">O exemplo a seguir obtém uma mensagem e, em seguida, a exclui:</span><span class="sxs-lookup"><span data-stu-id="288fa-152">The following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="288fa-153">Por padrão, uma mensagem só é oculta por 30 segundos; depois disso, fica visível para os outros clientes.</span><span class="sxs-lookup"><span data-stu-id="288fa-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="288fa-154">Você pode especificar um valor diferente usando `options.visibilityTimeout` com **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="288fa-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="288fa-155">Usar **getMessages** quando não existirem mensagens na fila não retornará um erro; no entanto, nenhuma mensagem será retornada.</span><span class="sxs-lookup"><span data-stu-id="288fa-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="288fa-156">Como: alterar o conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="288fa-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="288fa-157">Você pode alterar o conteúdo de uma mensagem na fila usando **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="288fa-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="288fa-158">O exemplo a seguir atualiza o texto de uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="288fa-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="288fa-159">Como adicionar opções para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="288fa-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="288fa-160">Há duas maneiras de personalizar a recuperação da mensagem de uma fila:</span><span class="sxs-lookup"><span data-stu-id="288fa-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="288fa-161">`options.numOfMessages` - recuperar um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="288fa-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="288fa-162">`options.visibilityTimeout` - definir um tempo limite de invisibilidade mais longo ou mais curto.</span><span class="sxs-lookup"><span data-stu-id="288fa-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="288fa-163">O seguinte exemplo usa o método **getMessages** para receber 15 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="288fa-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="288fa-164">Em seguida, ele processa cada mensagem usando um loop for.</span><span class="sxs-lookup"><span data-stu-id="288fa-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="288fa-165">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem retornada por este método.</span><span class="sxs-lookup"><span data-stu-id="288fa-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="288fa-166">Como obter o comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="288fa-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="288fa-167">O **getQueueMetadata** retorna metadados sobre a fila, incluindo o número aproximado de mensagens em espera na fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="288fa-168">Como: Listar Filas</span><span class="sxs-lookup"><span data-stu-id="288fa-168">How To: List Queues</span></span>
<span data-ttu-id="288fa-169">Para recuperar uma lista de filas, use **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="288fa-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="288fa-170">Para recuperar uma lista filtrada por um prefixo específico, use **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="288fa-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="288fa-171">Se não for possível retornar todas as filas, `result.continuationToken` poderá ser usado como o primeiro parâmetro de **listQueuesSegmented** ou o segundo parâmetro de **listQueuesSegmentedWithPrefix** para recuperar mais resultados.</span><span class="sxs-lookup"><span data-stu-id="288fa-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="288fa-172">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="288fa-172">How To: Delete a Queue</span></span>
<span data-ttu-id="288fa-173">Para excluir uma fila e todas as mensagens contidas nela, chame o método **deleteQueue** no objeto de fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="288fa-174">Para limpar todas as mensagens de uma fila sem excluí-la, use **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="288fa-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="288fa-175">Como: Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="288fa-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="288fa-176">Assinaturas de Acesso Compartilhado (SAS) são uma forma segura de fornecer acesso granular a filas sem fornecer o nome ou as chaves da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="288fa-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="288fa-177">As SAS são muitas vezes usadas para fornecer acesso limitado às filas, como permitir que um aplicativo móvel envie mensagens.</span><span class="sxs-lookup"><span data-stu-id="288fa-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="288fa-178">Um aplicativo confiável, como um serviço baseado em nuvem, gera uma SAS usando **generateSharedAccessSignature** de **QueueService**, e o oferece a um aplicativo não confiável ou semiconfiável.</span><span class="sxs-lookup"><span data-stu-id="288fa-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="288fa-179">Por exemplo, um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="288fa-179">For example, a mobile app.</span></span> <span data-ttu-id="288fa-180">A SAS é gerada utilizando uma política que descreve as datas inicial e final durante as quais a SAS é válida, assim como o nível de acesso concedido ao titular da SAS.</span><span class="sxs-lookup"><span data-stu-id="288fa-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="288fa-181">O exemplo a seguir gera uma nova política de acesso compartilhado que permitirá que o titular da SAS adicione mensagens à fila e expira 100 minutos após o momento em que é criado.</span><span class="sxs-lookup"><span data-stu-id="288fa-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="288fa-182">Observe que também devem ser fornecidas as informações do host, já que são necessárias quando o titular da SAS tenta acessar a fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="288fa-183">O aplicativo cliente usa a SAS com **QueueServiceWithSAS** para executar operações na fila.</span><span class="sxs-lookup"><span data-stu-id="288fa-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="288fa-184">O exemplo a seguir conecta à fila e cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="288fa-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="288fa-185">Como a SAS foi gerada com acesso para adição, se for feita uma tentativa de ler, atualizar ou excluir mensagens, será retornado um erro.</span><span class="sxs-lookup"><span data-stu-id="288fa-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="288fa-186">Listas de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="288fa-186">Access control lists</span></span>
<span data-ttu-id="288fa-187">Você também pode usar uma ACL (Lista de Controle de Acesso) para definir a política de acesso para uma SAS.</span><span class="sxs-lookup"><span data-stu-id="288fa-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="288fa-188">Isso é útil se você quiser permitir que vários clientes acessem a fila, mas oferece diferentes políticas de acesso para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="288fa-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="288fa-189">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="288fa-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="288fa-190">O seguinte exemplo define duas políticas: uma para 'user1' e outra para 'user2':</span><span class="sxs-lookup"><span data-stu-id="288fa-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="288fa-191">O exemplo a seguir obtém a ACL atual para **myqueue** e, em seguida, adiciona as novas políticas usando **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="288fa-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="288fa-192">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="288fa-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="288fa-193">Uma vez que a ACL foi definida, você pode criar uma SAS com base na ID de uma política.</span><span class="sxs-lookup"><span data-stu-id="288fa-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="288fa-194">O exemplo a seguir cria uma nova SAS para 'user2':</span><span class="sxs-lookup"><span data-stu-id="288fa-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="288fa-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="288fa-195">Next Steps</span></span>
<span data-ttu-id="288fa-196">Agora que você aprendeu os conceitos básicos do armazenamento de fila, siga estes links para saber mais sobre tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="288fa-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="288fa-197">Visite o [Blog da equipe de Armazenamento do Azure][Blog da equipe de Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="288fa-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="288fa-198">Visite o repositório [Microsoft Azure Storage SDK for Node.js][Azure Storage SDK for Node] (SDK do Armazenamento do Azure para Node.js) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="288fa-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="288fa-199">
[Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="288fa-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="288fa-200">[Aplicativo Web Node.js com o Serviço Tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="288fa-200">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="288fa-201">[Criar e implantar um aplicativo Node.js para um Serviço de Nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="288fa-201">[Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="288fa-202">[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/ [Criar e implantar um aplicativo Web Node.js no Azure usando a Matriz da Web]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="288fa-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
