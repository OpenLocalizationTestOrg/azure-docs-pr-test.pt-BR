---
title: "Introdução ao armazenamento de Filas do Azure usando o .NET | Microsoft Docs"
description: "As filas do Azure fornecem uma mensagem assíncrona e confiável entre os componentes do aplicativo. A mensagem na nuvem permite que os componentes do aplicativo se dimensionem de modo independente."
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
ms.openlocfilehash: 7f88aa9c50e669d1be7248346c7b1176bce61249
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="b333e-104">Introdução ao armazenamento de Fila do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="b333e-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="b333e-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b333e-105">Overview</span></span>
<span data-ttu-id="b333e-106">O armazenamento de filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b333e-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="b333e-107">Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente.</span><span class="sxs-lookup"><span data-stu-id="b333e-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="b333e-108">O armazenamento de filas fornece mensagens assíncronas para a comunicação entre os componentes do aplicativo, estando eles em execução na nuvem, na área de trabalho, em um servidor local ou em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="b333e-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="b333e-109">O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="b333e-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="b333e-110">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="b333e-110">About this tutorial</span></span>
<span data-ttu-id="b333e-111">Este tutorial mostra como gravar código .NET para alguns cenários comuns usando o armazenamento de Fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="b333e-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="b333e-112">Os cenários abordados incluem a criação e a exclusão de filas e a adição, a leitura e a exclusão de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="b333e-113">**Tempo estimado para conclusão:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="b333e-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="b333e-114">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="b333e-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="b333e-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b333e-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b333e-116">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="b333e-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="b333e-117">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="b333e-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="b333e-118">[Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b333e-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="b333e-119">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="b333e-119">Add using directives</span></span>
<span data-ttu-id="b333e-120">Adicione as seguintes diretivas `using` à parte superior do arquivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b333e-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="b333e-121">Analisar a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b333e-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="b333e-122">Criar o cliente do serviço Fila</span><span class="sxs-lookup"><span data-stu-id="b333e-122">Create the Queue service client</span></span>
<span data-ttu-id="b333e-123">A classe **CloudQueueClient** permite que você recupere as filas armazenadas no Armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="b333e-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="b333e-124">Veja uma maneira de criar o cliente de serviço:</span><span class="sxs-lookup"><span data-stu-id="b333e-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="b333e-125">Agora você está pronto para escrever um código que lê e grava dados no Armazenamento de Filas.</span><span class="sxs-lookup"><span data-stu-id="b333e-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="b333e-126">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="b333e-126">Create a queue</span></span>
<span data-ttu-id="b333e-127">Este exemplo mostra como criar uma fila se ela ainda não existe:</span><span class="sxs-lookup"><span data-stu-id="b333e-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="b333e-128">Inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="b333e-128">Insert a message into a queue</span></span>
<span data-ttu-id="b333e-129">Para inserir uma mensagem em uma fila existente, primeiro crie uma nova **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="b333e-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="b333e-130">Em seguida, chame o método **AddMessage** .</span><span class="sxs-lookup"><span data-stu-id="b333e-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="b333e-131">Um **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="b333e-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="b333e-132">Este é o código que cria uma fila (se ela não existir) e insere a mensagem 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="b333e-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="b333e-133">Espiar a próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="b333e-133">Peek at the next message</span></span>
<span data-ttu-id="b333e-134">Você pode inspecionar a mensagem na frente de uma fila sem removê-la da fila chamando o método **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="b333e-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="b333e-135">Alterar o conteúdo de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="b333e-135">Change the contents of a queued message</span></span>
<span data-ttu-id="b333e-136">Você pode alterar o conteúdo de uma mensagem in-loco na fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="b333e-137">Se a mensagem representar uma tarefa de trabalho, você poderá usar esse recurso para atualizar o status da tarefa de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b333e-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="b333e-138">O código a seguir atualiza a mensagem da fila com novo conteúdo e define o tempo limite de visibilidade para estender mais 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="b333e-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="b333e-139">Isso salva o estado do trabalho associado à mensagem e dá ao cliente mais um minuto para continuar trabalhando na mensagem.</span><span class="sxs-lookup"><span data-stu-id="b333e-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="b333e-140">Você pode usar essa técnica para acompanhar fluxos de trabalho de várias etapas em mensagens em fila, sem a necessidade de começar desde o início, caso uma etapa de processamento falhar devido a uma falha de hardware ou de software.</span><span class="sxs-lookup"><span data-stu-id="b333e-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="b333e-141">Normalmente, você mantém uma contagem de repetições e, se a mensagem for repetida mais de *n* vezes, você a exclui.</span><span class="sxs-lookup"><span data-stu-id="b333e-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="b333e-142">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="b333e-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="b333e-143">Remover a próxima mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="b333e-143">De-queue the next message</span></span>
<span data-ttu-id="b333e-144">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="b333e-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="b333e-145">Ao chamar **GetMessage**, você recebe a próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="b333e-146">Uma mensagem retornada de **GetMessage** torna-se invisível para todas as outras mensagens de leitura de código da fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="b333e-147">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="b333e-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="b333e-148">Para terminar de remover a mensagem da fila, você também deve chamar **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="b333e-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="b333e-149">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="b333e-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="b333e-150">Seu código chama **DeleteMessage** logo depois que a mensagem é processada.</span><span class="sxs-lookup"><span data-stu-id="b333e-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="b333e-151">Usar padrão Async-Await com APIs comuns de armazenamento da fila</span><span class="sxs-lookup"><span data-stu-id="b333e-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="b333e-152">Este exemplo mostra como usar o padrão Async-Await com APIs de armazenamento da fila comuns.</span><span class="sxs-lookup"><span data-stu-id="b333e-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="b333e-153">O exemplo chama a versão assíncrona de cada um dos métodos determinados, conforme indicado pelo sufixo *Async* de cada método.</span><span class="sxs-lookup"><span data-stu-id="b333e-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="b333e-154">Quando um método assíncrono é usado, o padrão async-await suspende a execução local até que a chamada seja concluída.</span><span class="sxs-lookup"><span data-stu-id="b333e-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="b333e-155">Esse comportamento permite que o thread atual faça outro trabalho que ajude a evitar gargalos de desempenho e melhora a capacidade de resposta geral do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b333e-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="b333e-156">Para obter mais detalhes sobre como usar o padrão Async-Await no .NET, confira [Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="b333e-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="b333e-157">Aproveitar opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="b333e-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="b333e-158">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="b333e-159">Primeiro, você pode obter um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="b333e-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="b333e-160">Segundo, você pode definir um tempo limite de invisibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="b333e-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="b333e-161">O exemplo de código a seguir usa o método **GetMessages** para receber 20 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b333e-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="b333e-162">Em seguida, ele processa cada mensagem usando um loop **foreach** .</span><span class="sxs-lookup"><span data-stu-id="b333e-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="b333e-163">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="b333e-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="b333e-164">Observe que os 5 minutos começam para todas as mensagens ao mesmo tempo; portanto, depois de 5 minutos desde a chamada para **GetMessages**, todas as mensagens que não tenham sido excluídas se tornarão visíveis novamente.</span><span class="sxs-lookup"><span data-stu-id="b333e-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="b333e-165">Obter o tamanho da fila</span><span class="sxs-lookup"><span data-stu-id="b333e-165">Get the queue length</span></span>
<span data-ttu-id="b333e-166">Você pode obter uma estimativa do número de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="b333e-167">O método **FetchAttributes** solicita que o serviço Fila recupere os atributos da fila, incluindo a contagem de mensagens.</span><span class="sxs-lookup"><span data-stu-id="b333e-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="b333e-168">A propriedade **ApproximateMessageCount** retorna o último valor recuperado pelo método **FetchAttributes**, sem chamar o serviço Fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="b333e-169">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="b333e-169">Delete a queue</span></span>
<span data-ttu-id="b333e-170">Para excluir uma fila e todas as mensagens que ela contém, chame o método **Delete** no objeto fila.</span><span class="sxs-lookup"><span data-stu-id="b333e-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="b333e-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b333e-171">Next steps</span></span>
<span data-ttu-id="b333e-172">Agora que você aprendeu os conceitos básicos do armazenamento de Fila, siga estes links para saber mais sobre tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="b333e-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="b333e-173">Consulte a documentação de referência do serviço Fila para obter detalhes completos sobre as APIs disponíveis:</span><span class="sxs-lookup"><span data-stu-id="b333e-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="b333e-174">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="b333e-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="b333e-175">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="b333e-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="b333e-176">Saiba como simplificar o código que você escreve para trabalhar com o Armazenamento do Azure usando o [SDK do Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b333e-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="b333e-177">Consulte outros guias de recursos para obter informações sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="b333e-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="b333e-178">[Introdução ao armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md) para armazenar dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="b333e-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="b333e-179">[Introdução ao armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) para armazenar dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="b333e-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="b333e-180">[Conectar-se ao Banco de Dados SQL usando .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) para armazenar dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="b333e-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
