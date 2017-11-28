---
title: "aaaGet de Introdução ao armazenamento de fila e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de fila do Azure em um projeto do ASP.NET Core no Visual Studio
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
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="70cff-103">Introdução ao armazenamento de filas e aos serviços conectados do Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="70cff-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="70cff-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="70cff-104">Overview</span></span>
<span data-ttu-id="70cff-105">Este artigo descreve como tooget iniciado usando o armazenamento de fila do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Olá Visual Studio **adicionar serviços conectados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70cff-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="70cff-106">Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="70cff-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="70cff-107">Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="70cff-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="70cff-108">Uma mensagem da fila única pode ser o too64 quilobytes (KB) de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="70cff-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="70cff-109">tooget iniciado, você primeiro precisa toocreate uma fila do Azure em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="70cff-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="70cff-110">Mostraremos como toocreate uma fila no código.</span><span class="sxs-lookup"><span data-stu-id="70cff-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="70cff-111">Também mostraremos como tooperform basic fila operações, como adicionar, modificar, ler e remover mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="70cff-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="70cff-112">exemplos de saudação são escritos em C\# de código e use Olá biblioteca de cliente de armazenamento do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="70cff-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="70cff-113">Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="70cff-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="70cff-114">**Observação:** alguns Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="70cff-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="70cff-115">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="70cff-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="70cff-116">código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="70cff-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="70cff-117">Consulte [Introdução ao Armazenamento de Filas do Azure usando .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações sobre como manipular filas com programação.</span><span class="sxs-lookup"><span data-stu-id="70cff-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="70cff-118">Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="70cff-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="70cff-119">Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="70cff-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="70cff-120">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="70cff-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="70cff-121">Acessar filas em código</span><span class="sxs-lookup"><span data-stu-id="70cff-121">Access queues in code</span></span>
<span data-ttu-id="70cff-122">filas de tooaccess em projetos do ASP.NET Core, você precisa fazer tooinclude Olá seguinte arquivo de origem do itens tooany c# que acessa o armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="70cff-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="70cff-123">Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.</span><span class="sxs-lookup"><span data-stu-id="70cff-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="70cff-124">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="70cff-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="70cff-125">Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="70cff-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="70cff-126">Obter um **CloudQueueClient** de objetos tooreference Olá fila na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="70cff-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="70cff-127">Obter um **CloudQueue** tooreference uma fila específica do objeto.</span><span class="sxs-lookup"><span data-stu-id="70cff-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="70cff-128">**Observação:** Use todos Olá acima código código Olá Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="70cff-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="70cff-129">Criar uma fila em código</span><span class="sxs-lookup"><span data-stu-id="70cff-129">Create a queue in code</span></span>
<span data-ttu-id="70cff-130">Olá toocreate fila do Azure no código, basta adicionar uma chamada muito**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="70cff-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="70cff-131">Adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="70cff-131">Add a message tooa queue</span></span>
<span data-ttu-id="70cff-132">tooinsert uma mensagem em uma fila existente, crie um novo **CloudQueueMessage** objeto, em seguida, chamada hello **AddMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="70cff-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="70cff-133">Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="70cff-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="70cff-134">Aqui está um exemplo que insere a mensagem de saudação 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="70cff-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="70cff-135">Ler uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="70cff-135">Read a message in a queue</span></span>
<span data-ttu-id="70cff-136">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="70cff-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="70cff-137">Ler e remover uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="70cff-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="70cff-138">Seu código pode remover uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="70cff-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="70cff-139">Chamar **GetMessageAsync** tooget Olá próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="70cff-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="70cff-140">Uma mensagem retornada de **GetMessageAsync** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="70cff-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="70cff-141">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="70cff-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="70cff-142">Removendo a mensagem de saudação de fila de hello, chamada de toofinish **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="70cff-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="70cff-143">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="70cff-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="70cff-144">chamadas de código a seguir Olá **DeleteMessageAsync** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="70cff-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="70cff-145">Como aproveitar opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="70cff-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="70cff-146">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="70cff-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="70cff-147">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="70cff-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="70cff-148">Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="70cff-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="70cff-149">usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="70cff-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="70cff-150">Em seguida, ele processa cada mensagem usando um loop **foreach** .</span><span class="sxs-lookup"><span data-stu-id="70cff-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="70cff-151">Ele também define minutos de too5 de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="70cff-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="70cff-152">Observe que Olá início de 5 minutos para todas as mensagens em Olá mesmo tempo, portanto, depois de 5 minutos após a chamada de saudação muito**GetMessages**, qualquer mensagem que não foram excluídas se tornar visível novamente.</span><span class="sxs-lookup"><span data-stu-id="70cff-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="70cff-153">Obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="70cff-153">Get hello queue length</span></span>
<span data-ttu-id="70cff-154">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="70cff-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="70cff-155">O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="70cff-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="70cff-156">Olá **ApproximateMethodCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="70cff-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="70cff-157">Usar padrão de saudação Async-Await com APIs de fila comum</span><span class="sxs-lookup"><span data-stu-id="70cff-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="70cff-158">Este exemplo mostra como toouse Olá Async-Await padrão com APIs de fila comum.</span><span class="sxs-lookup"><span data-stu-id="70cff-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="70cff-159">versão Olá exemplo chamadas Olá assíncrona de cada Olá fornecido métodos.</span><span class="sxs-lookup"><span data-stu-id="70cff-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="70cff-160">Isso pode ser visto por pós-correção de Olá assíncrona de cada método.</span><span class="sxs-lookup"><span data-stu-id="70cff-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="70cff-161">Quando um método assíncrono é usado, o padrão de Async-Await Olá suspende a execução local até Olá chamada ser concluída.</span><span class="sxs-lookup"><span data-stu-id="70cff-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="70cff-162">Esse comportamento permite Olá atual thread toodo outro trabalho que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70cff-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="70cff-163">Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET, consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="70cff-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="70cff-164">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="70cff-164">Delete a queue</span></span>
<span data-ttu-id="70cff-165">toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="70cff-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="70cff-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70cff-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

