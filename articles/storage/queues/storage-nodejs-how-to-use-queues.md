---
title: aaaHow toouse armazenamento de fila do Node. js | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Amostras escritas em Node.js."
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
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="cdeee-104">Como toouse armazenamento de fila do Node. js</span><span class="sxs-lookup"><span data-stu-id="cdeee-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="cdeee-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cdeee-105">Overview</span></span>
<span data-ttu-id="cdeee-106">Este guia mostra como os cenários comuns de tooperform usando Olá serviço de fila do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cdeee-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="cdeee-107">exemplos de saudação são gravados usando Olá API Node. js.</span><span class="sxs-lookup"><span data-stu-id="cdeee-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="cdeee-108">Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="cdeee-109">Criar um aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="cdeee-109">Create a Node.js Application</span></span>
<span data-ttu-id="cdeee-110">Criar um aplicativo Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="cdeee-110">Create a blank Node.js application.</span></span> <span data-ttu-id="cdeee-111">Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar um aplicativo da web Node. js no serviço de aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) usando o Windows PowerShell ou [ Criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="cdeee-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="cdeee-112">Configurar seu aplicativo tooAccess armazenamento</span><span class="sxs-lookup"><span data-stu-id="cdeee-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="cdeee-113">toouse armazenamento do Azure, você precisa hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="cdeee-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="cdeee-114">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain</span><span class="sxs-lookup"><span data-stu-id="cdeee-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="cdeee-115">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue toohello pasta em que você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cdeee-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="cdeee-116">Tipo **npm instalar o armazenamento do azure** na janela de comando hello.</span><span class="sxs-lookup"><span data-stu-id="cdeee-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="cdeee-117">A saída do comando de saudação é semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdeee-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="cdeee-118">Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="cdeee-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="cdeee-119">Dentro dessa pasta, você encontrará Olá **armazenamento do azure** pacote, que contém as bibliotecas de hello, você precisa acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cdeee-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="cdeee-120">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="cdeee-120">Import hello package</span></span>
<span data-ttu-id="cdeee-121">Usando o bloco de notas ou outro editor de texto, adicione Olá toohello superior a seguir o **server.js** arquivo de aplicativo hello onde você pretende toouse armazenamento:</span><span class="sxs-lookup"><span data-stu-id="cdeee-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="cdeee-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeee-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="cdeee-123">módulo de saudação do azure lerá variáveis de ambiente hello AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_conexão \_Cadeia de caracteres de informações necessárias tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdeee-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="cdeee-124">Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="cdeee-125">Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [Portal do Azure](https://portal.azure.com) para um site do Azure, consulte [Node. js web app usando] Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdeee-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="cdeee-126">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-126">How To: Create a Queue</span></span>
<span data-ttu-id="cdeee-127">Olá código a seguir cria um **QueueService** objeto, que permite que você toowork com filas.</span><span class="sxs-lookup"><span data-stu-id="cdeee-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="cdeee-128">Saudação de uso **createQueueIfNotExists** método, que retorna a fila especificada Olá se ela já existir, ou cria uma nova fila com o nome especificado da saudação se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="cdeee-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="cdeee-129">Se a fila de saudação é criada, `result.created` é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="cdeee-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="cdeee-130">Se a fila de saudação existir, `result.created` é false.</span><span class="sxs-lookup"><span data-stu-id="cdeee-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="cdeee-131">Filtros</span><span class="sxs-lookup"><span data-stu-id="cdeee-131">Filters</span></span>
<span data-ttu-id="cdeee-132">Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="cdeee-133">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="cdeee-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="cdeee-134">Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar" passando um retorno de chamada com hello assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeee-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="cdeee-135">Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou simplesmente chamar finalCallback tooend caso contrário, a saudação invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="cdeee-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="cdeee-136">Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="cdeee-137">Olá seguir cria um **QueueService** objeto que usa Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="cdeee-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="cdeee-138">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="cdeee-139">tooinsert uma mensagem em uma fila, use Olá **createMessage** método para criar uma nova mensagem e adicioná-lo toohello fila.</span><span class="sxs-lookup"><span data-stu-id="cdeee-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="cdeee-140">Como: Espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="cdeee-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="cdeee-141">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **peekMessages** método.</span><span class="sxs-lookup"><span data-stu-id="cdeee-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="cdeee-142">Por padrão, **peekMessages** inspeciona uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="cdeee-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="cdeee-143">Olá `result` contém a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeee-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="cdeee-144">Usando **peekMessages** quando não existem mensagens na fila de saudação não retornará um erro, mas nenhuma mensagem será retornada.</span><span class="sxs-lookup"><span data-stu-id="cdeee-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="cdeee-145">Como: Remover da fila Olá próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="cdeee-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="cdeee-146">O processamento de uma mensagem é um processo de duas fases:</span><span class="sxs-lookup"><span data-stu-id="cdeee-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="cdeee-147">Mensagem de saudação de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="cdeee-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="cdeee-148">Exclua mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeee-148">Delete hello message.</span></span>

<span data-ttu-id="cdeee-149">toodequeue uma mensagem, use **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="cdeee-150">Isso faz com que mensagens de saudação invisível na fila Olá, para que outros clientes não podem processá-los.</span><span class="sxs-lookup"><span data-stu-id="cdeee-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="cdeee-151">Depois que seu aplicativo tiver processado uma mensagem, chame **deleteMessage** toodelete-la da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeee-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="cdeee-152">saudação de exemplo a seguir obtém uma mensagem e exclui-lo:</span><span class="sxs-lookup"><span data-stu-id="cdeee-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="cdeee-153">Por padrão, uma mensagem apenas ficará oculta para 30 segundos, após o qual é visível tooother clientes.</span><span class="sxs-lookup"><span data-stu-id="cdeee-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="cdeee-154">Você pode especificar um valor diferente usando `options.visibilityTimeout` com **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="cdeee-155">Usando **getMessages** quando não existem mensagens na fila de saudação não retornará um erro, mas nenhuma mensagem será retornada.</span><span class="sxs-lookup"><span data-stu-id="cdeee-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="cdeee-156">Como: Alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="cdeee-157">Você pode alterar o conteúdo de saudação de um mensagem no local Olá fila usando **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="cdeee-158">saudação de exemplo a seguir atualiza o texto de saudação de uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="cdeee-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="cdeee-159">Como adicionar opções para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="cdeee-160">Há duas maneiras de personalizar a recuperação da mensagem de uma fila:</span><span class="sxs-lookup"><span data-stu-id="cdeee-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="cdeee-161">`options.numOfMessages`-Recuperar um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="cdeee-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="cdeee-162">`options.visibilityTimeout` - definir um tempo limite de invisibilidade mais longo ou mais curto.</span><span class="sxs-lookup"><span data-stu-id="cdeee-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="cdeee-163">Olá, exemplo a seguir usa Olá **getMessages** mensagens tooget 15 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="cdeee-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="cdeee-164">Em seguida, ele processa cada mensagem usando um loop for.</span><span class="sxs-lookup"><span data-stu-id="cdeee-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="cdeee-165">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para todas as mensagens retornadas por este método.</span><span class="sxs-lookup"><span data-stu-id="cdeee-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="cdeee-166">Como Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="cdeee-167">Olá **getQueueMetadata** retorna metadados sobre a fila de hello, incluindo o número aproximado de mensagens aguardando na fila de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="cdeee-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="cdeee-168">Como: Listar Filas</span><span class="sxs-lookup"><span data-stu-id="cdeee-168">How To: List Queues</span></span>
<span data-ttu-id="cdeee-169">tooretrieve uma lista de filas, use **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="cdeee-170">tooretrieve uma lista filtrada por um prefixo específico, use **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="cdeee-171">Se todas as filas não podem ser retornadas, `result.continuationToken` pode ser usado como Olá primeiro parâmetro de **listQueuesSegmented** ou Olá segundo parâmetro de **listQueuesSegmentedWithPrefix** tooretrieve mais resultados.</span><span class="sxs-lookup"><span data-stu-id="cdeee-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="cdeee-172">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="cdeee-172">How To: Delete a Queue</span></span>
<span data-ttu-id="cdeee-173">toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **deleteQueue** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeee-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="cdeee-174">tooclear todas as mensagens de uma fila sem excluí-la, use **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="cdeee-175">Como: Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="cdeee-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="cdeee-176">Assinaturas de acesso compartilhado (SAS) são uma tooqueues de acesso granular de tooprovide de maneira segura sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="cdeee-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="cdeee-177">SAS geralmente são as filas tooyour de acesso usados tooprovide limitado, como permitir que um aplicativo móvel toosubmit mensagens.</span><span class="sxs-lookup"><span data-stu-id="cdeee-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="cdeee-178">Um aplicativo confiável como um serviço baseado em nuvem gera uma SAS usando Olá **generateSharedAccessSignature** de saudação **QueueService**e fornece-tooan aplicativos de confiança parcial ou não confiável.</span><span class="sxs-lookup"><span data-stu-id="cdeee-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="cdeee-179">Por exemplo, um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="cdeee-179">For example, a mobile app.</span></span> <span data-ttu-id="cdeee-180">Olá SAS é gerado usando uma política, que descreve o início de saudação e datas finais durante o qual Olá SAS é válido, bem como Olá detentor SAS do nível toohello concedido acesso.</span><span class="sxs-lookup"><span data-stu-id="cdeee-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="cdeee-181">saudação de exemplo a seguir gera uma nova política de acesso compartilhado que permitirá Olá a fila SAS detentor tooadd mensagens toohello e expira 100 minutos após o tempo de saudação que é criado.</span><span class="sxs-lookup"><span data-stu-id="cdeee-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="cdeee-182">Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando detentor SAS Olá tentativas de fila de saudação tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cdeee-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="cdeee-183">Olá aplicativo cliente, em seguida, usa Olá SAS com **QueueServiceWithSAS** tooperform operações em fila hello.</span><span class="sxs-lookup"><span data-stu-id="cdeee-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="cdeee-184">saudação de exemplo a seguir conecta-se a fila de toohello e cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="cdeee-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="cdeee-185">Desde que hello SAS foi gerado com acesso de adicionar, se uma tentativa foi feita tooread, atualizar ou excluir mensagens, um erro será retornado.</span><span class="sxs-lookup"><span data-stu-id="cdeee-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="cdeee-186">Listas de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="cdeee-186">Access control lists</span></span>
<span data-ttu-id="cdeee-187">Você também pode usar uma política de acesso de saudação de tooset de lista de controle de acesso (ACL) para uma SAS.</span><span class="sxs-lookup"><span data-stu-id="cdeee-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="cdeee-188">Isso é útil se você quiser tooallow várias filas de saudação tooaccess de clientes, mas fornece as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="cdeee-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="cdeee-189">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="cdeee-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="cdeee-190">saudação de exemplo a seguir define duas políticas; um para 'user1' e outro para o 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="cdeee-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="cdeee-191">Olá obtém de exemplo a seguir Olá ACL atual para **myqueue**, em seguida, adiciona novas políticas de saudação usando **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="cdeee-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="cdeee-192">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="cdeee-192">This approach allows:</span></span>

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

<span data-ttu-id="cdeee-193">Uma vez Olá que ACL tiver sido definido, você pode criar uma SAS com base na ID de saudação de uma política.</span><span class="sxs-lookup"><span data-stu-id="cdeee-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="cdeee-194">saudação de exemplo a seguir cria uma nova SAS para 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="cdeee-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="cdeee-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cdeee-195">Next Steps</span></span>
<span data-ttu-id="cdeee-196">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cdeee-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="cdeee-197">Visite Olá [Azure Storage Team Blog] [Blog da equipe do armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="cdeee-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="cdeee-198">Visite Olá [SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="cdeee-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="cdeee-199">
[Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="cdeee-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="cdeee-200">[Aplicativo de web Node. js usando Olá serviço tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="cdeee-200">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="cdeee-201">[Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="cdeee-201">[Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="cdeee-202">[Blog da equipe do armazenamento do azure]: http://blogs.msdn.com/b/windowsazurestorage/ [compilar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="cdeee-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
