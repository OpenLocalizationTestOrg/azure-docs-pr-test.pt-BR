---
title: "aaaGet de Introdução ao armazenamento de fila do Azure usando o .NET | Microsoft Docs"
description: "As filas do Azure fornecem uma mensagem assíncrona e confiável entre os componentes do aplicativo. Nuvem permite que mensagens seu tooscale de componentes de aplicativo independentemente."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="ebff6-104">Introdução ao armazenamento de Fila do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="ebff6-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="ebff6-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ebff6-105">Overview</span></span>
<span data-ttu-id="ebff6-106">O armazenamento de filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ebff6-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="ebff6-107">Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente.</span><span class="sxs-lookup"><span data-stu-id="ebff6-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="ebff6-108">Armazenamento de fila fornece mensagens assíncronas para a comunicação entre componentes de aplicativos, quer eles estejam em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="ebff6-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="ebff6-109">O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="ebff6-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="ebff6-110">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="ebff6-110">About this tutorial</span></span>
<span data-ttu-id="ebff6-111">Este tutorial mostra como toowrite .NET código em alguns cenários comuns usando o armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebff6-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="ebff6-112">Os cenários abordados incluem a criação e a exclusão de filas e a adição, a leitura e a exclusão de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="ebff6-113">**Estimado tempo toocomplete:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="ebff6-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="ebff6-114">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="ebff6-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="ebff6-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebff6-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="ebff6-116">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="ebff6-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="ebff6-117">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="ebff6-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="ebff6-118">[Uma conta do Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ebff6-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="ebff6-119">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="ebff6-119">Add using directives</span></span>
<span data-ttu-id="ebff6-120">Adicione o seguinte Olá `using` superior de toohello de diretivas de saudação `Program.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="ebff6-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="ebff6-121">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="ebff6-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="ebff6-122">Criar o cliente do serviço de fila Olá</span><span class="sxs-lookup"><span data-stu-id="ebff6-122">Create hello Queue service client</span></span>
<span data-ttu-id="ebff6-123">Olá **CloudQueueClient** classe permite que você tooretrieve filas armazenadas no armazenamento de fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="ebff6-124">Aqui está o cliente do serviço Olá toocreate unidirecional:</span><span class="sxs-lookup"><span data-stu-id="ebff6-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="ebff6-125">Agora você está pronto toowrite código lê e grava o armazenamento de tooQueue de dados.</span><span class="sxs-lookup"><span data-stu-id="ebff6-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="ebff6-126">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-126">Create a queue</span></span>
<span data-ttu-id="ebff6-127">Este exemplo mostra como toocreate uma fila se ela ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="ebff6-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="ebff6-128">Inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-128">Insert a message into a queue</span></span>
<span data-ttu-id="ebff6-129">tooinsert uma mensagem em uma fila existente, primeiro crie um novo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="ebff6-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="ebff6-130">Em seguida, chame Olá **AddMessage** método.</span><span class="sxs-lookup"><span data-stu-id="ebff6-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="ebff6-131">Um **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="ebff6-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="ebff6-132">Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="ebff6-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="ebff6-133">Espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="ebff6-133">Peek at hello next message</span></span>
<span data-ttu-id="ebff6-134">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessage** método.</span><span class="sxs-lookup"><span data-stu-id="ebff6-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="ebff6-135">Alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="ebff6-136">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebff6-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="ebff6-137">Se a mensagem representa uma tarefa de trabalho, você pode usar tooupdate esse recurso o status da tarefa de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="ebff6-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="ebff6-138">saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="ebff6-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="ebff6-139">Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebff6-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="ebff6-140">Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="ebff6-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="ebff6-141">Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="ebff6-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="ebff6-142">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="ebff6-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="ebff6-143">Eliminação da fila de mensagem de saudação do próxima</span><span class="sxs-lookup"><span data-stu-id="ebff6-143">De-queue hello next message</span></span>
<span data-ttu-id="ebff6-144">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="ebff6-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="ebff6-145">Quando você chama **GetMessage**, obter próxima mensagem de saudação em uma fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="ebff6-146">Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="ebff6-147">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="ebff6-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="ebff6-148">toofinish mensagem de saudação remover da fila hello, você também deve chamar **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="ebff6-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="ebff6-149">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="ebff6-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="ebff6-150">Seu código chama **DeleteMessage** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="ebff6-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="ebff6-151">Usar padrão Async-Await com APIs comuns de armazenamento da fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="ebff6-152">Este exemplo mostra como Olá toouse Async-Await padrão com APIs comuns de armazenamento de fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="ebff6-153">exemplo Hello chama a versão assíncrona saudação de cada Olá fornecido métodos, conforme indicado pelo Olá *Async* sufixo de cada método.</span><span class="sxs-lookup"><span data-stu-id="ebff6-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="ebff6-154">Quando um método assíncrono é usado, Olá async-await padrão suspende a execução local até Olá chamada ser concluída.</span><span class="sxs-lookup"><span data-stu-id="ebff6-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="ebff6-155">Esse comportamento permite Olá atual thread toodo outro trabalho, o que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ebff6-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="ebff6-156">Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="ebff6-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="ebff6-157">Aproveitar opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="ebff6-158">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="ebff6-159">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="ebff6-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="ebff6-160">Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="ebff6-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="ebff6-161">usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="ebff6-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="ebff6-162">Em seguida, ele processa cada mensagem usando um loop **foreach** .</span><span class="sxs-lookup"><span data-stu-id="ebff6-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="ebff6-163">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="ebff6-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="ebff6-164">Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**GetMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.</span><span class="sxs-lookup"><span data-stu-id="ebff6-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="ebff6-165">Obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="ebff6-165">Get hello queue length</span></span>
<span data-ttu-id="ebff6-166">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="ebff6-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="ebff6-167">O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebff6-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="ebff6-168">Olá **ApproximateMessageCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebff6-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="ebff6-169">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="ebff6-169">Delete a queue</span></span>
<span data-ttu-id="ebff6-170">toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebff6-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="ebff6-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebff6-171">Next steps</span></span>
<span data-ttu-id="ebff6-172">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ebff6-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="ebff6-173">Exiba a documentação de referência de serviço de fila de saudação para obter detalhes completos sobre as APIs disponíveis:</span><span class="sxs-lookup"><span data-stu-id="ebff6-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="ebff6-174">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="ebff6-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="ebff6-175">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="ebff6-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="ebff6-176">Saiba como código de saudação toosimplify escrever toowork com armazenamento do Azure usando Olá [SDK do Azure WebJobs](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ebff6-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="ebff6-177">Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="ebff6-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="ebff6-178">[Introdução ao armazenamento de tabela do Azure usando o .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore estruturado de dados.</span><span class="sxs-lookup"><span data-stu-id="ebff6-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="ebff6-179">[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="ebff6-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="ebff6-180">[Conecte-se tooSQL banco de dados usando o .NET (c#)](../../sql-database/sql-database-connect-query-dotnet-core.md) dados relacionais toostore.</span><span class="sxs-lookup"><span data-stu-id="ebff6-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
