---
title: "aaaGet de Introdução ao armazenamento de fila e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de fila do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="c4e36-103">Introdução aos serviços conectados do armazenamento de Fila do Azure e Visual Studio (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="c4e36-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c4e36-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c4e36-104">Overview</span></span>
<span data-ttu-id="c4e36-105">Este artigo descreve como tooget iniciado usando o armazenamento de fila do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto de serviços de nuvem usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="c4e36-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="c4e36-106">Mostraremos como toocreate uma fila no código.</span><span class="sxs-lookup"><span data-stu-id="c4e36-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="c4e36-107">Também mostraremos como tooperform basic operações, como adicionar, modificar, ler e remoção de fila de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="c4e36-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="c4e36-108">exemplos de saudação são escritos em código c# e usam Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4e36-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="c4e36-109">Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="c4e36-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="c4e36-110">Consulte a [Introdução ao Armazenamento de Filas do Azure usando o .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para obter mais informações sobre a manipulação de filas no código.</span><span class="sxs-lookup"><span data-stu-id="c4e36-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="c4e36-111">Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e36-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="c4e36-112">Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e36-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="c4e36-113">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c4e36-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="c4e36-114">Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c4e36-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c4e36-115">Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4e36-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="c4e36-116">Acessar filas em código</span><span class="sxs-lookup"><span data-stu-id="c4e36-116">Access queues in code</span></span>
<span data-ttu-id="c4e36-117">filas de tooaccess em projetos de serviços de nuvem do Visual Studio, você precisa fazer tooinclude Olá seguinte arquivo de origem tooany c# de itens que acessar o armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e36-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="c4e36-118">Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.</span><span class="sxs-lookup"><span data-stu-id="c4e36-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="c4e36-119">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4e36-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4e36-120">Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e36-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="c4e36-121">Obter um **CloudQueueClient** de objetos tooreference Olá fila na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4e36-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="c4e36-122">Obter um **CloudQueue** tooreference uma fila específica do objeto.</span><span class="sxs-lookup"><span data-stu-id="c4e36-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="c4e36-123">**Observação:** Use todos Olá acima código código Olá Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4e36-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="c4e36-124">Criar uma fila em código</span><span class="sxs-lookup"><span data-stu-id="c4e36-124">Create a queue in code</span></span>
<span data-ttu-id="c4e36-125">fila de saudação toocreate no código, basta adicionar uma chamada muito**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="c4e36-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="c4e36-126">Adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="c4e36-126">Add a message tooa queue</span></span>
<span data-ttu-id="c4e36-127">tooinsert uma mensagem em uma fila existente, crie um novo **CloudQueueMessage** objeto, em seguida, chamada hello **AddMessage** método.</span><span class="sxs-lookup"><span data-stu-id="c4e36-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="c4e36-128">Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="c4e36-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="c4e36-129">Aqui está um exemplo que insere a mensagem de saudação 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="c4e36-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="c4e36-130">Ler uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="c4e36-130">Read a message in a queue</span></span>
<span data-ttu-id="c4e36-131">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessage** método.</span><span class="sxs-lookup"><span data-stu-id="c4e36-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="c4e36-132">Ler e remover uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="c4e36-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="c4e36-133">Seu código pode remover uma mensagem de uma fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c4e36-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="c4e36-134">Chamar **GetMessage** tooget Olá próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="c4e36-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="c4e36-135">Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="c4e36-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="c4e36-136">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="c4e36-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="c4e36-137">Removendo a mensagem de saudação de fila de hello, chamada de toofinish **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="c4e36-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="c4e36-138">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="c4e36-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="c4e36-139">chamadas de código a seguir Olá **DeleteMessage** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="c4e36-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="c4e36-140">Use opções adicionais tooprocess e remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="c4e36-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="c4e36-141">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="c4e36-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="c4e36-142">Você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="c4e36-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="c4e36-143">Você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="c4e36-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="c4e36-144">usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="c4e36-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="c4e36-145">Em seguida, ele processa cada mensagem usando um loop **foreach** .</span><span class="sxs-lookup"><span data-stu-id="c4e36-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="c4e36-146">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="c4e36-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="c4e36-147">Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**GetMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.</span><span class="sxs-lookup"><span data-stu-id="c4e36-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="c4e36-148">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4e36-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="c4e36-149">Obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="c4e36-149">Get hello queue length</span></span>
<span data-ttu-id="c4e36-150">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="c4e36-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="c4e36-151">O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e36-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="c4e36-152">Olá **ApproximateMethodCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e36-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="c4e36-153">Usar saudação padrão Async-Await com APIs comuns de fila do Azure</span><span class="sxs-lookup"><span data-stu-id="c4e36-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="c4e36-154">Este exemplo mostra como Olá toouse Async-Await padrão com APIs comuns de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e36-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="c4e36-155">exemplo Hello chama a versão assíncrona de saudação de cada Olá fornecido métodos, isso pode ser visto por Olá **Async** após a correção de cada método.</span><span class="sxs-lookup"><span data-stu-id="c4e36-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="c4e36-156">Quando um método assíncrono é usado Olá async-await padrão suspende a execução local até Olá chamada ser concluída.</span><span class="sxs-lookup"><span data-stu-id="c4e36-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="c4e36-157">Esse comportamento permite Olá atual thread toodo outro trabalho que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4e36-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="c4e36-158">Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="c4e36-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="c4e36-159">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="c4e36-159">Delete a queue</span></span>
<span data-ttu-id="c4e36-160">toodelete uma fila e todas as mensagens de saudação contidas nele, chamada hello **excluir** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e36-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="c4e36-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4e36-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

