---
title: "Introdução ao armazenamento de filas e aos serviços conectados do Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Como começar a usar o armazenamento de filas do Azure em um projeto ASP.NET Core no Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="af391-103">Introdução ao armazenamento de filas e aos serviços conectados do Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="af391-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="af391-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="af391-104">Overview</span></span>
<span data-ttu-id="af391-105">Este artigo descreve como começar a usar o Armazenamento de Filas do Azure no Visual Studio depois de ter criado ou referenciado uma conta de Armazenamento do Azure em um projeto ASP.NET Core usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af391-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="af391-106">A operação **Adicionar Serviços Conectados** instala os pacotes NuGet apropriados para acessar o armazenamento do Azure no seu projeto e adiciona a cadeia de conexão para a conta de armazenamento aos arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="af391-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="af391-107">O armazenamento de filas do Azure é um serviço para armazenamento de um grande número de mensagens que podem ser acessadas de qualquer lugar do mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="af391-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="af391-108">Uma única mensagem de fila pode ter até 64 KB (kilobytes) de tamanho e uma fila pode conter milhões de mensagens, até o limite de capacidade total de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af391-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="af391-109">Para começar, primeiramente, você precisa criar uma fila do Azure em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af391-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="af391-110">Mostraremos como criar uma fila em código.</span><span class="sxs-lookup"><span data-stu-id="af391-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="af391-111">Também mostraremos como realizar operações básicas de fila, como adicionar, modificar, ler e remover entidades de fila.</span><span class="sxs-lookup"><span data-stu-id="af391-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="af391-112">Os exemplos são escritos em C\# e usam a biblioteca do cliente de armazenamento do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="af391-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="af391-113">Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="af391-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="af391-114">**OBSERVAÇÃO:** algumas APIs que executam chamadas para o armazenamento do Azure no ASP.NET Core são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="af391-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="af391-115">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="af391-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="af391-116">O código a seguir pressupõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="af391-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="af391-117">Consulte [Introdução ao Armazenamento de Filas do Azure usando .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações sobre como manipular filas com programação.</span><span class="sxs-lookup"><span data-stu-id="af391-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="af391-118">Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="af391-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="af391-119">Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="af391-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="af391-120">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="af391-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="af391-121">Acessar filas em código</span><span class="sxs-lookup"><span data-stu-id="af391-121">Access queues in code</span></span>
<span data-ttu-id="af391-122">Para acessar filas em projetos do ASP.NET Core, você precisa incluir os itens a seguir para qualquer arquivo de origem de C# que acessa o armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="af391-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="af391-123">Verifique se as declarações de namespace na parte superior do arquivo de C# incluem estas instruções de **uso** .</span><span class="sxs-lookup"><span data-stu-id="af391-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="af391-124">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af391-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="af391-125">Use o seguinte código para obter a sua cadeia de conexão de armazenamento e informações de conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="af391-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="af391-126">Obtenha um objeto **CloudQueueClient** para referenciar objetos de fila em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af391-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="af391-127">Obtenha um objeto **CloudQueue** para referenciar uma fila específica.</span><span class="sxs-lookup"><span data-stu-id="af391-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="af391-128">**OBSERVAÇÃO:** use todo esse código antes do código nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="af391-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="af391-129">Criar uma fila em código</span><span class="sxs-lookup"><span data-stu-id="af391-129">Create a queue in code</span></span>
<span data-ttu-id="af391-130">Para criar a fila do Azure no código, basta adicionar uma chamada para **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="af391-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="af391-131">Adicionar uma mensagem a uma fila</span><span class="sxs-lookup"><span data-stu-id="af391-131">Add a message to a queue</span></span>
<span data-ttu-id="af391-132">Para inserir uma mensagem em uma fila existente, crie primeiro um novo objeto **CloudQueueMessage** e depois chame o método **AddMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="af391-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="af391-133">Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="af391-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="af391-134">Aqui está um exemplo que insere a mensagem “Hello, World”.</span><span class="sxs-lookup"><span data-stu-id="af391-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="af391-135">Ler uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="af391-135">Read a message in a queue</span></span>
<span data-ttu-id="af391-136">Você pode espiar a mensagem na frente de uma fila sem removê-la da fila, chamando o método **PeekMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="af391-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="af391-137">Ler e remover uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="af391-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="af391-138">Seu código pode remover uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="af391-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="af391-139">Chame **GetMessageAsync** para obter a próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="af391-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="af391-140">Uma mensagem retornada de **GetMessageAsync** torna-se invisível para todas as outras mensagens de leitura de código desta fila.</span><span class="sxs-lookup"><span data-stu-id="af391-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="af391-141">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="af391-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="af391-142">Para concluir a remoção da mensagem da fila, chame **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="af391-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="af391-143">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="af391-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="af391-144">O código a seguir chamará **DeleteMessageAsync** logo depois que a mensagem tiver sido processada.</span><span class="sxs-lookup"><span data-stu-id="af391-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="af391-145">Como aproveitar opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="af391-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="af391-146">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="af391-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="af391-147">Primeiro, você pode obter um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="af391-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="af391-148">Segundo, você pode definir um tempo limite de invisibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="af391-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="af391-149">O exemplo de código a seguir usa o método **GetMessages** para receber 20 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="af391-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="af391-150">Em seguida, ele processa cada mensagem usando um loop **foreach** .</span><span class="sxs-lookup"><span data-stu-id="af391-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="af391-151">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="af391-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="af391-152">Lembre-se de que os 5 minutos começam para todas as mensagens ao mesmo tempo, portanto, após 5 minutos desde a chamada para **GetMessages**, todas as mensagens que não foram excluídas se tornarão visíveis novamente.</span><span class="sxs-lookup"><span data-stu-id="af391-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="af391-153">Obter o tamanho da fila</span><span class="sxs-lookup"><span data-stu-id="af391-153">Get the queue length</span></span>
<span data-ttu-id="af391-154">Você pode obter uma estimativa do número de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="af391-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="af391-155">O método **FetchAttributes** solicita que o serviço Fila recupere os atributos da fila, incluindo a contagem de mensagens.</span><span class="sxs-lookup"><span data-stu-id="af391-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="af391-156">A propriedade **ApproximateMethodCount** retorna o último valor recuperado pelo método **FetchAttributes**, sem chamar o serviço Fila.</span><span class="sxs-lookup"><span data-stu-id="af391-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="af391-157">Usar o padrão Async-Await com APIs comuns de fila</span><span class="sxs-lookup"><span data-stu-id="af391-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="af391-158">Este exemplo mostra como usar o padrão Async-Await com APIs de fila comuns.</span><span class="sxs-lookup"><span data-stu-id="af391-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="af391-159">O exemplo chama a versão assíncrona de cada um dos métodos determinados.</span><span class="sxs-lookup"><span data-stu-id="af391-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="af391-160">Isso pode ser visto pela pós-correção de Async de cada método.</span><span class="sxs-lookup"><span data-stu-id="af391-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="af391-161">Quando um método assíncrono é usado, o padrão Async-Await suspende a execução local até que a chamada seja concluída.</span><span class="sxs-lookup"><span data-stu-id="af391-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="af391-162">Esse comportamento permite que o thread atual faça outro trabalho que ajude a evitar gargalos de desempenho e melhora a capacidade de resposta geral do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="af391-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="af391-163">Para obter mais detalhes sobre como usar o padrão Async-Await no .NET, confira [Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="af391-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="af391-164">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="af391-164">Delete a queue</span></span>
<span data-ttu-id="af391-165">Para excluir uma fila e todas as mensagens que ela contém, chame o método **Delete** no objeto fila.</span><span class="sxs-lookup"><span data-stu-id="af391-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="af391-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af391-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

